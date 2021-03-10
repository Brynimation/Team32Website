## 23/11/2020 – 29/11/2020

This week we finished the video walk-through of our prototype and sent to Dean to critique. He liked our GUI, saying its “very well thought out” and said it could be extended easily for additional features (i.e., adding an option to allow radiologists to see the actual DICOM scans could be included as a button on the left panel). However, he wants us to add the GOSH, Intel and and UCL logos to the menu page. He also wants the video to be updated to show our Figma prototype as it might look on a laptop or 2 in 1 device, specifically one that uses an intel CPU.

This required us to make a few adjustments to our prototype (the main considerations being that a user may be using an
actual keyboard rather than a touchscreen keyboard in order to write the annotations, but also purely layout-based instructions
due to the change in screen size). The second video wasn’t too difficult to produce as we were able to re-use large portions of the audio from the original.
[Here's the first video](https://drive.google.com/drive/u/0/my-drive) and [Here's the second video](https://drive.google.com/file/d/1c14WkA9pfw4MGd1ClSsJz1fGz7yjVFV5/view?usp=sharing)  

In our weekly team meeting on Friday we were joined by Dr Arthur Owens, a radiologist at the NHS, and Dr Richard Price of Health Education England. 
We played our video walkthrough, and discussed in further detail how HEE might want to make use of our system, one of these involving the development of a RESTful API.
We have another meeting booked in with Dr Owens for next Thursday in order to gain further insight into the kind of UI that would suit a radiologist using the system.  

A number of our requirements feel quite tentative and difficult to tackle without further guidance at the moment. However, certain “Must Have” requirements are concrete. As such, we’ve started to look at implementing elements of the UI in separate unity scenes to combine later (Bryn – camera controls and accessing individual layers of the organ at run time, Daniel – looking at how to change the transparency of different layers, Yuan Shuai – General work on the UI).
<br>
Ran into a minor problem with git – doesn’t support the pushing of files above a certain size which our glb organ models unfortunately exceed. 
We later fixed this by installing Github Large File Storage (glfs), and configuring it to track our example glb models.
