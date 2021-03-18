## 30/11/2020 – 6/12/2020

This week’s focus was working on the Unity project itself, as we want something we can show by the end of term.  
* We added the functionality to select which segment to view exclusively. This is a step towards the segment selector that we want and will eventually tie in with the rest of the UI. As the brain model as 5 segments, we have 5 segment buttons in our temporary GUI, each of which selects one of the segments. 
        
*LoadBrain.cs*
```     
      List<GameObject> segments = new List<GameObject>();
      GameObject brain;
          ...
      void Start(){
        brain = Siccity.GLTFUtility.Importer.LoadFromFile(filepath);
          ...
        foreach(Transform child in brain.transform){
            segments.Add(child.gameObject);
        }
      }
          ...
       for(int i = segments.Count - 1; i !=-1; i--){
            if(segments[i].GetComponent<Renderer>() != null)enabledRenderers.Push((segments[i].GetComponent<Renderer>()));
        }
    }
    public void disableRenderer(){
        if(enabledRenderers.Count !=0){
            Debug.Log("disabled");
            enabledRenderers.Peek().enabled = false;
            disabledRenderers.Push(enabledRenderers.Pop());
        }
    }
    public void enableRenderer(){
        if(disabledRenderers.Count !=0){
            Debug.Log("enabled");
            disabledRenderers.Peek().enabled = true;
            enabledRenderers.Push(disabledRenderers.Pop());
        }
    }
```
* The disableRender and enableRenderer functions are passed as callbacks to two buttons in our GUI.
* We added the functionality to change the opacity of one segment. We're doing this by passing the function below as a callback to a Unity slider. We’ve run into a visual bug where segments seem to appear/disappear when being viewed through a transparent segment, and hope to find a way to fix this.
```   
    public float SegOpacity = 0.8f;
    ...
    public void AdjustOpacity(float newOp) {
        SegOpacity = newOp;
        segments[0].GetComponent<MeshRenderer>().material.color = new Color(1.0f, 1.0f, 1.0f, SegOpacity)
        
 ```

We also  had a meeting with an NHS radiologist, Owen Arthurs, to gather insight from someone who has experience with DICOM scan software, and also had a good idea of what would be required in an application such as the one we’re developing. 
We were guided through the Windows software he used, which can display DICOM scans taken from multiple angles together, and contains features we’re still looking to implement such as adding annotations. We recorded the meeting to look back on for future reference. 
One big distinction is that the radiology software he used is for mouse and keyboard control, while our application should support touchscreen use, so we have to do some things differently. However, based on our discussion with Dean last week, the fact that Intel is our main client suggests that building a mobile version of the application is less important than getting something that works on an intel based laptop.
Although we made good progress in regards to the segment selection functionality this week, we ran into a pretty significant problem on creating our first actual Unity Build. Up to this point we had been testing the functionality of our system within the Unity editor exclusively, which was an error. The model wouldn’t load in the actual build. This required an enormous of debugging and ate into the time we could’ve spent looking into implementing other features. The issue was due to 2 things:
* Shaders included in the GLTFUtility library were not set to be added to builds by default.
* GLTFUtility relies on Json.NET which requires  .NET 4.0 compatibility or greater, while our Unity project only had .NET 2.0 compatibility.
Changing both of these things was trivial, but figuring out that they were the problem took a very long time. However, it’s good that we encountered this issue relatively early and now that it’s fixed, it shouldn’t re-emerge as an issue.
