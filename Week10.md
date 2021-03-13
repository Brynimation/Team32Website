## 14/12/2020 – 21/12/2020
As was mentioned in the blog post last week, there were some big issues with our opacity slider feature. We spent a good portion of this week trying to resolve the problem.
In doing some research we found that the problem wasn't in the c# script that we wrote that adjusts the opacity, but was rather an issue with the shader used to create the material that gets applied to the meshes at runtime.
The shader is part of the GLTFUtility library that we're using to load gltf/glb models into Unity at run-time. There is nothing inherently wrong with the shader; the issue stems from attempting to draw multiple, complex, transparent objects that are over the top of one another to the screen at once. 

[This document](https://docs.unity3d.com/Manual/SL-CullAndDepth.html) in the Unity manual was very helpful, and lead us to including an additional Pass in the shader that forces the GPU to write to the Z-buffer. <br><br>

*Pass{  
  Zwrite On  
  colour depth 0  
}*  <br><br>
*By default, when the "RenderType" tag of a shader is set to "Transparent", the GPU does not write to the zBuffer.*<br><br>
This did actually prevent the strange visual glitches that we got with the old shader, but unfortunately had the effect of outer segments of the model completely hiding the inner segments. Even when the outermost segment had its opacity very low, and the segments below it were opaque, the segments below it could not be seen.  
So we wrote a function to m adjust the renderingQueue attribute of the material applied to each segment of the model being loaded in at runtime, such that the innermost segments are drawn later (so are applied a material with a higher renderingQueue value).   
This solved the previous problem, but then we were faced with the opposite issue. The parts of the outer segment that are covered by the inner segments are not drawn to the screen, so when adjusting the opacity of an inner segment the outer segment appears to be full of holes. This issue isn't too noticable until the opacity of the inner segment goes below a certain value. So now, if the opacity of a segment is set to below a certain *minOpacity*, then its renderer is disabled altogether so that the segment behind it is rendered entirely.<br><br>
The solution certainly isn't perfect, but rendering semi-transparent objects is a [known problem in Unity](https://answers.unity.com/questions/609021/how-to-fix-transparent-rendering-problem.html), so I think our solution is sufficient for the time being.
