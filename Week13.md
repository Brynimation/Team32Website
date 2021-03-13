## 04/01/2021 – 11/01/2021

This week my main focus was on beginning to make Shuai’s new UI design functional in preparation for our elevator pitch. The goal of this was not to implement every aspect of every single feature, but to have a number of features that we can at least show are clearly under development for our pitch. By the end of the week, I had successfully managed to incorporate our existing functionality into Shuai’s new UI design. I was initially unsure of how to do this.  

Helpfully, whenever a canvas is created in the hierarchy of a scene in Unity, an automatically generated EventSystem object is produced, which keeps track of the position of the cursor and which UI elements are clicked. It does this using a “GraphicsRayCaster” component. I therefore made the decision to look further into how events work in Unity and C# and wrote the “SelectionManager” class, which maintains a reference to all the buttons in the scene and fires off an appropriate event whenever a button is selected. The benefit of using events is that it makes use of the publisher/subscriber pattern. Meaning, I can have as many other classes (or observers) subscribe to the events that are fired off as I want without modifying any existing code; the SelectionManager class is unaware of the classes subscribed to it. I hope that this will make our system more easily extensible to additional features.
[This video](https://www.youtube.com/watch?v=OuZrhykVytg&t=611s), [this video](https://www.youtube.com/watch?v=G5R4C8BLEOc) and [these documents](https://docs.microsoft.com/en-us/dotnet/standard/events/) were very helpful.  

Furthermore, I also started work on the annotation feature. The user can now press the bottom-most button on the left-hand side, drag a pin onto the model and an annotation that the user can fill in will pop up.

I was able to keep the code for this relatively concise by extending interfaces offered by the UnityEngine.UI namespace, namely IDragHandler and IDropHandler.  
<br>
**picture of code goes here**

At the moment, the text entered by the user doesn’t go anywhere meaningful (it’s just output to the console when the “confirm” button is pressed). However, I’m pleased with the progress from an interactivity and visual standpoint.

Over the week we met up a number of times via MS teams in order to get a plan and script ready for our elevator pitch. Along with the live delivery of the pitch we need to produce a pre-recorded video whose contents will be the same as the pitch. We have a script and all the slides ready, bar a video demonstrating the application running. We plan to record this, along with our pre-recorded video, next week.
