## 01/02/2021 – 07/02/2021

An aspect of the cross sectional viewer feature which I hadn’t had time to look at last week was the controls. <br>
As the shader works by determining what is above and what is below a plane, I thought it made sense to allow the user to control a plane using sliders: one for its y position above the model, and three for the 3 axes of rotation. I also used the reference shaders to create another shader that, instead of culling any polygons of the model above the plane, changes their colour to black. I think this works well as a means of visualising what will be removed and what will be kept after the cross section is created.

[Here's what it looks like](https://drive.google.com/file/d/1v0BmrBsi1qSZWK5kpbs3UGAvCHc6DCz-/view?usp=sharing)

In our meeting on Thursday our clients seemed very happy with the cross sectional slicing feature, which was a huge relief given how long it took to get right.  
Over the weekend I spent some time updating the start page to allow the user to select from one of our five example models from a drop-down menu, rather than only being able to view the brain.  
On Sunday I was also asked by Dr Mohemedally to get a build of our project in its current state to him by the following evening, complete with a splash screen and the names of our team members and supervisors on the start page.
