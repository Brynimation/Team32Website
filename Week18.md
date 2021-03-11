
## 08/02/2021 - 14/02/2021
After having delivered our first build to our clients (at the request of Dr Mohamedally - who wanted our application to be used to demonstrate the capabilities of a final year student's project, which involves touch-less gesture technology), my main focus this week was on allowing our application to work beyond the example models we were given.  

There were two aspects to this problem: Allowing the user to browse local storage to find a model to load into the application, and ensuring that the camera controls work as expected with a range of different models.  

To solve the former problem I spent some time looking into some plugins that we could make use of, and [found one on the Unity Asset Store that suited our needs perfectly.](https://github.com/gkngkc/UnityStandaloneFileBrowser).

Our example models are loaded into the application with a hard-coded position and orientation relative to a parent GameObject that sits at the origin (0,0,0). Our camera controls are such that they rotate about the transform of this parent GameObject. This slight offset from the origin isn't strictly necessary, but as our models are complex (have many children as well as visual artifacts that can span quite far from the model's true centre), the position that Unity calculates to be their centre/transform felt un-intuitive and lead to the camera controls feeling equally un-intuitive.
The offset we applied corrected this, but this isn't a good approach in a general sense.

So instead of having the camera centred explicitly about this parent GameObject, the camera is instead centred about a pivot point that is initialised to a position of (0,0,0). The user can then change the position of this pivot point by means of three sliders, one slider for each of its axes in 3D space.   

In our meeting on Friday Dr Mohemedally asked that I add the ability to move the camera using keybinds. However, it should not just move left, right,up,down, but more as if it is rotating about a sphere whose centre is far beyond the position of our model. The rotation about the model when using the mouse should still look as if the camera is centred about it (or wherever the pivot is), even if the camera has been rotated about this imaginary sphere. This sounds very difficult but I will look into it.

In testing some [open source glb/gltf files](https://github.com/KhronosGroup/glTF-Sample-Models). I found that in most cases the camera controls were fine when centred about (0,0,0), but having the pivot controller certainly helped if ever they didn't. The pivot controller also lets the user have more freedom over exactly what they want to focus on (eg, they can centre the camera about one of two kidneys).  


However, an issue that presented itself when loading in these models was how much smaller and larger models can be than the ones we've been experimenting with. This lead to models seeming like they hadn't been loaded in at all, but were just too small to be seen from the camera's current position. This is an issue to be thought about in the coming week.

