## 16/11/2020 – 22/11/2020

This week we pushed our first unity test to the GitHub Repository. Unity is a relatively new technology to all of us, although a few of us are familiar with it and have used it a little bit before.  

One of the first issues we had was the fact that Unity does not support GLB/GLTF files natively (only working with .obj and .fbx), so we spent some time looking into libraries that allow GLB/GLTF models to be imported at runtime.

[This is the one we've chosen.](https://nicedoc.io/Siccity/GLTFUtility)  

Using this library, we were able to import and render a GLB file at runtime. It’s important that we work with the models at runtime, as in an ideal world our system will have FHIR interoperability. Therefore, our system must be capable of receiving GLTF/GLB files via this protocol, rather than simply accessing a model from local storage.
The library seems to work well for the model we used but, we need to keep in mind that the kinds of models we’ll actually be dealing with will be significantly more complex and will have multiple layers and so we’ll need to determine if the library is suitable once we have access to more appropriate models.
One of our clients and module lead, Dr Dean Mohemadally, has suggested we create a video walk-through of our Figma prototype in order to show off its potential features to our target users (eg, Doctors, clinicians, radiologists and other NHS workers).  

He’s willing to distribute the video to people in the NHS on our behalf as a means of gathering requirements(we don’t have permission to gather requirements directly from people in the NHS but he does). This will be extremely helpful for us, as this prototype was created based on the feedback of pseudo-users rather than our true target users.
