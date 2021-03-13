## 26/01/2021 – 31/01/2021

This week my focus was on getting the most difficult aspect of the organ slicing feature implemented, ie actually being able to remove of parts of the rendered model in order to see cross sections of the organ. I have not yet put too much thought into the best way to make this feature usable.

Having tested the mesh-slicing library that my TA sent me on primitive GameObjects last week, I decided to try using it on the Brain model which we have been working with. Unfortunately, due to the difference in the number of vertices between a cube (which has eight vertices) and the Brain model we’re using (which has over 600 000 vertices), it was not possible to slice the mesh in this way. Attempting to slice the mesh lead to Unity crashing. Having to process this much graphical data using a CPU bound process simply isn’t feasible.

Therefore, I needed to look much further into shaders. Although we have had to deal with shaders in order to allow the opacity of our meshes to be changed via a slider, we just made minimal changes to the shaders the models were using by default and didn’t require us to look into the inner-workings of shaders too deeply.  
Thankfully, we did not need to create the new shader we needed from scratch. Not only did we have a lot of reference material to use in the GLTFUtility library, but Unity provides templates for a number of different types of shader written in **High-Level Shader Language** (HLSL). The materials applied to the models currently use a kind of shader known as a [surface shader](https://docs.unity3d.com/Manual/SL-SurfaceShaders.html). These are written in HLSL, and automatically generate more low level *vertex* and *fragment* shaders that actually run on the GPU.  

The concept we needed to employ in our shader is similar to *occlusion culling*, in which an object will only be rendered if it is between the near and far *clipping planes* of the camera. If an object is partially between these two planes, only its polygons between the two planes will be drawn to the screen.  

[One open source shader that I found](https://github.com/Dandarawy/Unity3DCrossSectionShader/blob/master/Assets/Cross%20Section%20Shader/Shaders/OnePlaneBSP.shader) proved that what we need to do has been done before. It works by calculating the dot product of:  
  * a plane's normal and 
  * the distance between the current vertex on the mesh and the plane's position.  
If the result is positive, then the current pixel being processed is above the plane (so can be discarded).  

This shader did work well, but unfortunately its rendering mode was set to Opaque so did not support our transparency changing features. Just changing the rendering mode to transparent lead to a number of very strange effects as expected. The fix that I used the first time we encountered this problem (Turning the ZWrite On and ColorMask to 0 in a Pass) lead to other issues, namely that many parts of the cross section were occluded.

Truthfully, writing a shader that supported both the cross sectional view feature and our opacity feature was quite experimental, but it works.<br><br>
One important thing to note is that the Shader has two properties related to the plane: *_planeNormal* and *_planePosition*, but these are just arbitrary Vector3 values. In order to test the shader, I've been using a plane GameObject as a means of visualising the plane, where its transform.position is passed as the _planePosition property, and its transform.up attribute is passed as the _planeNormal property. The values of these properties are updated every frame.

