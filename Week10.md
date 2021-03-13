## 14/12/2020 – 21/12/2020
As was mentioned in the blog post last week, there were some big issues with our opacity slider feature. We spent a good portion of this week trying to resolve the problem.
In doing some research we found that the problem wasn't in the c# script that we wrote that adjusts the opacity, but was rather an issue with the shader used to create the material that gets applied to the meshes at runtime.
The shader is part of the GLTFUtility library that we're using to load gltf/glb models into Unity at run-time. There is nothing inherently wrong with the shader; the issue stems from attempting to draw multiple, overlaid, complex, transparent objects to the screen at once. 

[This document](https://docs.unity3d.com/Manual/SL-CullAndDepth.html) in the Unity manual was very helpful, and lead us to including an additional Pass in the shader that forces the GPU to write to the Z-buffer. By default, shaders whose renderingMode is transparent do not write to the zBuffer.<br><br>
*Pass{  
  Zwrite On  
  colour depth 0  
}*  <br><br>
This did actually prevent the strange glitches that we were seeing when moving the camera with the old shader applied, but unfortunately had the effect of outer segments of the model completely hiding the inner segments. Even when the outermost segment had its opacity very low, and the segments below it were opaque, the segments below it could not be seen.  
So we wrote a function to manually adjust the renderingQueue attribute of the material applied to each segment of the model being loaded in at runtime, such that the innermost segments are drawn later (so are applied a material with a higher renderingQueue value).  
This solved the previous problem, but now changing the opacity of an inner segment has some effects on segments above it. The effects are much less of an issue, however.  
It seems that rendering complex transparent objects is a problem that's documented as being difficult, so I think for the time being our solution will work just fine. We have too many requirements for us to spend too much longer on this issue alone.
