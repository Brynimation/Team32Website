# 01/02/2021-07/02/2021 - DICOM viewer and Tooltips
Unfortunately we encountered an issue with the DICOM library. I was previously unaware that all Healthcare/NHS projects had to be AGPL-V3 licensed, and fo-dicom was licensed under MS-PL. The two licenses are incompatible, so I had to spend sometime looking for another suitable library.  
Many of the AGPL-V3 compatible libaries for DICOM viewing written in C# were either long abandonned or built for .NET applications, so would not work in Unity.  
The library I ended up using was the SimpleImageToolKit (SITK). SITK is not just for loading DICOMs, but for medical image/medical model data in geneal.
The solution using this library was less trivial. It involved first reading the .dcm file in as a SITKImage. This image is then written to a png and loaded back into
a Texture2D object. The implementation from this stage onwards was the same.    
Along with this, I made some changes to the github and its readme to ensure that all necessary dependencies are cloned when the repo itself is cloned.  
Finally, I spent the remainder of the week adding documentation to our code.
