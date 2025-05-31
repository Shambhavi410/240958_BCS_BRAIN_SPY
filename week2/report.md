# MRI Data Visualization - Report

## Description of Approach

- Loading NIfTI files using the `nibabel` library and inspecting their metadata and structure.
- Reading a series of DICOM files using `pydicom`, extracting relevant metadata, and stacking slices to form a 3D volume.
- Visualizing different anatomical planes (axial, sagittal, coronal) using `matplotlib`.
- Understanding and comparing image orientation via affine matrices (NIfTI) and orientation tags (DICOM).
- Discussing the differences between DICOM and NIfTI formats in terms of structure, use-case, and tooling.

## Q1: How can we read and load NIfTI and DICOM files in Python?

For NIfTI:
```python
import nibabel as nib
nifti_img = nib.load('Sample_Data/sample.nii.gz')
nifti_data = nifti_img.get_fdata()
```

For DICOM:
```python
import pydicom
import os
dicom_dir = "Sample_Data/DICOM/"
slices = [pydicom.dcmread(os.path.join(dicom_dir, f)) for f in os.listdir(dicom_dir) if f.endswith('.dcm')]
```

## Q2: What is the internal structure and metadata of these formats?

NIfTI:
- Shape: `nifti_data.shape`
- Affine matrix: `nifti_img.affine`
- Header: Contains voxel dimensions, data type, timing info, etc.

DICOM:
- Example fields:
```python
sample = slices[0]
sample.PatientName
sample.Modality
sample.PixelSpacing
sample.SliceThickness
sample.ImagePositionPatient
```

## Q3: How do we stack DICOM slices into a 3D volume?

Steps:
1. Read all DICOM slices in a folder.
2. Sort using `ImagePositionPatient[2]` or `InstanceNumber`.
3. Stack using numpy.

```python
import numpy as np
slices.sort(key=lambda s: float(s.ImagePositionPatient[2]))
dicom_volume = np.stack([s.pixel_array for s in slices], axis=0)
```

## Q4: How can we visualize anatomical planes from a 3D image volume?

Static views of axial, coronal, and sagittal planes were created using `matplotlib`.

```python
import matplotlib.pyplot as plt

def show_plane(volume, axis, index, title):
    if axis == 'axial':
        img = volume[index, :, :]
    elif axis == 'coronal':
        img = volume[:, index, :]
    elif axis == 'sagittal':
        img = volume[:, :, index]
    plt.imshow(img, cmap='gray')
    plt.title(title)
    plt.axis('off')
    plt.colorbar()
    plt.show()

# Example:
show_plane(dicom_volume, 'axial', dicom_volume.shape[0] // 2, "Axial Plane")
```

## Q5: How do we interpret image orientation?

For NIfTI:
- Affine matrix maps voxel indices to real-world coordinates.
```python
print(nifti_img.affine)
```

For DICOM:
- `ImageOrientationPatient` gives direction cosines.
- `ImagePositionPatient` gives slice origin.

Understanding both is essential to interpret the orientation and alignment of the image in 3D space.

## Q6: What are the key differences between DICOM and NIfTI?

| Feature              | DICOM                                 | NIfTI                               |
|----------------------|----------------------------------------|--------------------------------------|
| Purpose              | Clinical use                          | Research (neuroimaging)             |
| Structure            | Multiple .dcm files (one per slice)   | Single file (.nii or .nii.gz)       |
| Metadata             | Extensive, per-slice                  | Compact, centralized in header      |
| Orientation          | Direction cosines, position tags      | Affine matrix                       |
| Tooling in Python    | Manual stacking required              | Easy loading and access             |

## Screenshot of Visualizations
![image](https://github.com/user-attachments/assets/e3dbe6eb-db78-42ae-8aa6-8b7b9e3d92d5)

## Notes on Preprocessing or Assumptions Made

- DICOM slices were assumed to be from a single series with uniform spacing.
- Sorting was performed using `ImagePositionPatient[2]`.
- preprocessing included slice-wise intensity normalization, scaling pixel values linearly to the 0-255 range before converting to 16-bit unsigned integers for DICOM storage.
- NIfTI files were directly loaded using nibabel, with no orientation correction applied.

## Observations and Challenges Encountered

- DICOM slices can come unordered; sorting is critical to form a valid 3D volume.
- Some DICOM files may be missing key tags or may contain inconsistencies.
- NIfTI is simpler to work with for research due to its unified structure and metadata handling.
- Visualization using matplotlib worked well for static inspection, but interactive tools could enhance usability.
