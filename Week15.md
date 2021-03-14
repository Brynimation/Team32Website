## 19/01/2021 - 25/01/2021
This week, we were able to finish the implementation of the colour palette, and also store the state of the scene (camera coordinates, model segment colours, etc) and the annotation text when a user creates an annotation.  

In implementing the colour palette, we split the problem into two sub-problems and wrote a class to address each one:  
* the movement of the colour palette -> paletteMovement
* selecting a colour from the colour palette -> colourSelector

The paletteMovement script implements the IDragHandler interface. If the user clicks on the palette, the angle between the cursor and the centre of the palette between frames is calculated. The palette is then rotated by this amount around the z-axis.<br><bt>
 *This next bit was written when I was very tired so I need to update it*<br>
The colourSelector script required more research. The colour palette png was imported into unity as a Texture2D object. We have access to the underlying pixel data of the Texture2D via the GetPixel() method, which returns the colour of a pixel at a specified screenspace coordinate. However, cslling GetPixel with the mouse's current position as a parameter does not work. The mouse is in screen space, but we need the pixel in texture space.  
In Unity, screen space starts from (0,0) at the bottom left and ends at (screenWidth, screenHeight) in the top right. The colours array however, is a flattened 2D array, so we needed to adjust the position of our mouse accordingly using the *RectTransformUtility.ScreenToLocalPointInRect* method.
With the mouse position updated for texture space, we needed to calculate whether the time between clicks was less than some constant *DOUBLE_CLICK_TIME*. If it is, then an event containing the colour is sent from the ColourSelector class to update the currently selected mesh of the model. otherwise nothing happens
