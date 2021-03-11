## 26/01/2021 – 31/01/2021

This week my focus was on getting the most difficult aspect of the organ slicing feature implemented, ie actually being able to remove of parts of the rendered model in order to see cross sections of the organ. I have not yet put too much thought into the best way to make this feature usable.

Having tested the mesh-slicing library that my TA sent me on primitive GameObjects last week, I decided to try using it on the Brain model which we have been working with. Unfortunately, due to the difference in the number of vertices between a cube (which has eight vertices) and the Brain model we’re using (which has over 600 000 vertices), it was not possible to slice the mesh in this way. Having to process this much graphical data using a CPU bound process simply isn’t feasible.

Therefore, I needed to look much further into shaders. Although we have had to deal with shaders in order to allow the opacity of our meshes to be changed via a slider, we just made minimal changes to the shaders the models were using by default and didn’t require us to look into the inner-workings of shaders too deeply.

The type of shader that I needed to accomplish the slicing of the organ was a “clipping plane shader”, which would render all polygons on one side of a plane but not the other, allowing a cross section of the organ to be seen.

[One that I found worked extremely well](https://github.com/Dandarawy/Unity3DCrossSectionShader/blob/master/Assets/Cross%20Section%20Shader/Shaders/OnePlaneBSP.shader), bar the fact that changing the opacity would lead to similar draw-order issues that we experienced when first attempting to implement the transparency feature. The fix that I used the first time we encountered this problem (Turning the ZWrite On and ColorMask to 0 in a Pass) lead to other issues, namely that many parts of the cross section were occluded.

Writing a shader that worked was extremely experimental and involved a lot of trial and error, but it does the trick.
