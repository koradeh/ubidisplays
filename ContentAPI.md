# Introduction #

There are two main types of toolkit software. The first type is the toolkit _application software_—responsible for hardware configuration, interactive surface layout, and content deployment. The second type is _items of content_—responsible for application specific graphics and behaviour.

## Writing to the debug log (Authority.log) ##

This is used to log data to the toolkit debug menu.
```
// Write data to the debug log.
Authority.log("Some data")
```

## Invoking methods across displays (Authority.call) ##

This is used to communicate across displays.  Imagine you have two displays: `"Surface 0"` and `"Surface 1"`. When `Surface 0` is pressed, it tells `Surface 1` to react somehow.

`Surface 0`
```
...
      <script type="text/javascript">
         // Once the page has loaded, create a presence detector.
         $(document).ready(function()
         {
            // Create a new presence detector called 'area'.
            //   0.1m high with a 0.02m offset.
            var pd = new PresenceDetector("area", 0.1, 0.02);
            
            // Tell the other display
            pd.onStateChange = function(state){
               
               Authority.call("Surface 1", "myFunction", state);
               
            }
         };
      </script>
...
```

`Surface 1`
```
...
      <script type="text/javascript">
         
         // This will be called by Surface 0.
         function myFunction(callingSurface, data) {
                  // Do something here!
         }
      </script>
...
```

## Invoking toolkit methods (Authority.request) ##

The _Content API_ is a way of letting items of content communicate with the toolkit application and each other.

All the items listed with the 'C# API' label are accessed through the Authority.request mechanism.  All of them items listed with the 'JS API' label are implemented in JavaScript and imported as normal.

```
      <script type="text/javascript">
         
         // Once the page has loaded this is possible.
         $(document).ready(function()
         {
             Authority.request("movedisplay", { target : "Surface 1"})
         }   

      </script>
```

|**Function Name**|**API**|**Documentation**|
|:----------------|:------|:----------------|
|swapdisplay      |C# API |Swap this display with one on another surface. Content on the target surface will be moved to the calling surface.

&lt;BR&gt;

 target: The name of the Surface which this display content should jump too.|
|movedisplay      |C# API |Move the calling display to another surface. This will fail if content is already present on the target surface.

&lt;BR&gt;

 target: The name of the Surface which this display content should jump too.

&lt;BR&gt;

 force\_reload: Should the display content be re-loaded during the move, or remain active.|
|swaptargetdisplay|C# API |Swap a display on a target surface with another target surface.

&lt;BR&gt;

 target1: The name of surface which contains the display to be moved.

&lt;BR&gt;

 target2: The name of the surface which will receive the display.|
|movetargetdisplay|C# API |Move a target display from one surface to another. 

&lt;BR&gt;

 source: The name of surface which contains the display to be moved.

&lt;BR&gt;

 dest: The name of the surface which will receive the display.

&lt;BR&gt;

 override: Should content on the destination surface be closed. True of False.

&lt;BR&gt;

 force\_reload: Should the display content be re-loaded during the move, or remain active.|
|closedisplay     |C# API |Close the calling display.  This will delete the display from the deployment model and free up all its resources.|
|closetargetdisplay|C# API |Close the display on a given surface. 

&lt;BR&gt;

 target: The name of the Surface which is currently showing the display to be closed.|
|surfacelist      |C# API |Return a list of surface names active in the current deployment model back to the calling display.

&lt;BR&gt;

 callback: The JS function to be called back with the results.|
|surfaceinfo      |C# API |Return information about a surface.

&lt;BR&gt;

 surfaces: An array of string surface names to get the information for. E.g. ["Surface 0"].

&lt;BR&gt;

 callback: The JS function to be called back with the results. Returns a dictionary of results with surface names as keys.  Missing names are not returned.|
|playsound        |C# API |Play a sound at a specified file.  This is deprecated - use HTML5 audio tags where possible.

&lt;BR&gt;

 file: The path to the sound file to play.|
|opendisplay      |C# API |Open a display on another surface.

&lt;BR&gt;

 target: The name of the surface which the content should be opened on.

&lt;BR&gt;

load: The 'load instruction' (i.e. URL) which should be opened on the new surface.

&lt;BR&gt;

 override: A Boolean which determines if any existing content on the target surface should be closed.|
|kinectlowestpointcube|C# API |Create a lowest point cube and attach it as a display resource.

&lt;BR&gt;

 relativeto: The name of the surface to detect points relative too (i.e. above the current surface).

&lt;BR&gt;

 callback: The function in the display content which will be called with the results.  It will accept data in the format: [[x,y,z],...]

&lt;BR&gt;

 surface\_zoffset: The offset from the surface to start detecting points.

&lt;BR&gt;

 height: The height at which to stop detecting points (+the offset).

&lt;BR&gt;

 point\_limit: The maximum number of points to send in any one frame.

&lt;BR&gt;

 sendemptyframes: Should empty data frames be sent.

&lt;BR&gt;

 sendemptysucessiveframes: Should empty data frames AFTER the first empty frame be sent.

&lt;BR&gt;

|
|Convert\_P2M     |JS API |Converts x pixels to meters for the display that calls it

&lt;BR&gt;

 value: The number of pixels to convert. E.g. 100 or 2.23

&lt;BR&gt;

 axis: The dimension to convert using.  "w" for width. "h" for height.

&lt;BR&gt;

 return: The resultant number of meters for 'value' pixels.|
|Convert\_M2P     |JS API |Converts x meters to pixels for the display that calls it

&lt;BR&gt;

 value: The number of meters to convert. E.g. 0.2 or 2

&lt;BR&gt;

 axis: The dimension to convert using.  "w" for width. "h" for height.

&lt;BR&gt;

 return: The resultant number of pixels for 'value' pixels.|
|PresenceDetector |JS API |A presence detector function that will check for the presence of an object in a particular area above (or below) a display surface. 

&lt;BR&gt;

 sName: A unique name for this detector. e.g. "low", "middle" or "high", or "switch".

&lt;BR&gt;

 fHeight: The height of the area in meters above the display. In meters.

&lt;BR&gt;

 fOffset: The offset from the surface to start detecting at. In meters.

&lt;BR&gt;

 iCountLimit: The number of points required for a solid detection.

&lt;BR&gt;

Usage:

&lt;BR&gt;

`var pd = new PresenceDetector("area", 0.1, 0.02);`

&lt;BR&gt;

`pd.onFound       = function() { console.log("present"); }`

&lt;BR&gt;

`pd.onLost        = function() { console.log("not present"); }`

&lt;BR&gt;

`pd.onStateChange = function(bState) { console.log(bState); }`|
|KinectTouch      |JS API |A class which adds multi-touch to a page.  Uses the same control arguments as 'kinectlowestpointcube' with the following additional parameters:

&lt;BR&gt;

 debug: Should the touch detector render each touch point using a coloured circle.  True for yes. False for no.

&lt;BR&gt;

 trails: Should the touch detector render each point in the point cloud detected above the surface. True for yes.  False for no.

&lt;BR&gt;

Usage:

&lt;BR&gt;

`var kt = new KinectTouch({ debug : true, height : 0.02 });`|


## Working with Physical Sizes (Surface.XXX and Surface\_PropertiesChanged) ##

You can access the physical properties of the Surface through variables on the `Surface` object.
Like the `Authority` object, the `Surface` object is created by the toolkit when the page loads.  It is also kept up-to-date when any Surface properties change.  You cannot set values, but you can get them via this interface.  If you want to be notified when the physical surface properties change, you can implement the `Surface_PropertiesChanged` function, as below.

```
...
/** This function is run by the toolkit when the *physical* surface properties change. */
function Surface_PropertiesChanged()
{
	// Print the surface name.
	Authority.log("" + Surface.Name);
	
	// Print the surface dimensions.
	Authority.log("" + round(Surface.Width, 2) + "m x " + round(Surface.Height, 2) + "m");
	
	// Print the surface angle.
	Authority.log("" + round(Surface.Angle * 57.2957795, 2) + " degrees");
	
	// Apply fancy physical responsive design rules.
	if (Surface.Width < 0.1)
	{
		$("body").addClass("smallscreen");
	}
...
```