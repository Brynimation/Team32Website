## 07/12/2020 – 13/12/2020

We decided to streamline our development process by using Unity Teams Collaboration and Cloud Build. Cloud Build automatically builds the project every time a new change is made to the project. All 3 of us get an email detailing the changes of the most recent commit.
![](./Images/Week3/Email.png)  
This has also reduced a healthy level of redundancy into our workflow, since we essentially have two remote repositories for our project. On the off-chance that something goes horribly wrong with one of them, we'll be safe as the other one will still exist. We just need to remember to push to both. 
* The segment selector is now tied to the opacity slider, so the opacities of all layers can be adjusted individually, as well as being able to view them all individually. We now have 5 buttons in our scene that each select one of the 5 different segments of the brain. 
``` 
    int currentlySelected = 0;
    ...
    public void AdjustOpacity(float newOp) {
        if(currentlySelected != -1){
            segOpacity = newOp;
            Color color = segments[currentlySelected].seg.GetComponent<MeshRenderer>().material.color;
            color.a = segOpacity;
            segments[currentlySelected].seg.GetComponent<MeshRenderer>().material.color = color;
        }
    }
```
* We've also started to think about how we might implement annotations. We were thinking we might have to implement a user input field from scratch, but Unity provides a type *TMP_InputField* in the *TMP* (TextMeshPro) namespace which handles the user input side of things for us. This is good news.
* We had another meeting with our clients, where we showed our progress by screen sharing. Some new ideas have been brought up, and previous ones expanded upon. For example, Costas suggested the idea of a plane that can be cut through the model to view a sort of cross section of the model. We’ve also been told to look further into RESTful API, such that a link can open our app and show a specific model, perhaps from a specific angle with specific annotations.  
