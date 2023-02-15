# Using multiple monitors<a name="using-multiple-screens"></a>

DCV is capable of extending full screen resolution across a single monitor, a set of selected monitors, or all available monitors\.

You can also manually specify custom display layouts\. For more information, see [ Managing the NICE DCV Session Display Layout](https://docs.aws.amazon.com/dcv/latest/adminguide/managing-session-display.html) in the *NICE DCV Administrator Guide*\.

**Note**  
If the requested layout is not supported by the server, the layout might be adjusted to match the display limits of your server\. If the layout cannot be adjusted, the request fails and the changes are not applied\.

**Extending full\-screen across all monitors**  
You can use the NICE DCV clients to extend the display for a session across multiple monitors and be able to set each display to full screen resolution\.

With the Windows, Linux, and macOS clients, the extended display matches your physical display layout and screen resolutions\. 

With the web browser client, the session display can be extended to up to two screens with 1920x1080 screen resolution\. When the display is extended, the additional screen is opened in a new browser window\. The second extends the display to the right of the original screen\. Ensure that you position the screens accordingly\.

**Example**  
For example, three monitors are connected to your local computer\. The server extends the display for a session across all three monitors and matches the specific screen resolutions of your display\.

To enable this feature, do one of the following depending on your client\.
+ **Windows client**

  1. Go to the toolbar at the top of the window\.

  1. Choose the **Full Screen** icon\.

  1. Select **Across all monitors** from the drop\-down menu\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/Full_screen_all_windows.png)
+ **macOS client**

  1. Go to the toolbar at the top of the window\.

  1. Choose **View** from the toolbar at the top of window\.

  1. Select **Full Screen All Monitors** from the drop\-down menu\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/macos-extend.png)
+ **Linux client**

  1. Go to the toolbar at the top of the window\.

  1. Choose the **Full Screen** icon\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/full_screen_linux.png)
+ **Web browser client**

  1. Go to the toolbar at the top of the window\.

  1. Choose the **Multiscreen** icon\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/web-multiscreen.png)

**Extending full\-screen across selected monitors**  
If there are three or more monitors connected, DCV can also extend full\-screen across a selection of those available monitors\. If your selected monitors cannot go full screen, an error message will appear and you will need to perform the procedure again\.

**Note**  
This feature is currently on Windows clients for Windows based sessions only\.
+ **Windows client**

  1. Go to the top menu\.

  1. Select the **Full Screen** icon\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/Full_screen_selected_windows.png)

  1. Select **Across selected monitors** from the drop down menu\.
**Note**  
The **Across selected monitors** window will appear displaying your current monitor layout\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/Windows_client_mulitple_monitors.png)

     Monitors must be set adjacent, or sharing a side with each other, in your Windows display setting\.

     *Examples of adjacent monitor placement\.*
**Note**  
The blue boxes are DCV enabled monitors\.  
The gray boxes are other monitors\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/multi-monitors-yes.png)

     *Examples of nonadjacent monitor placement\.*  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/multi-monitors-no.png)

     If your monitors are not set adjacent in your Windows display configuration, you will need to exit DCV and change your Display settings on your local machine\.

  1. Select which monitors you want DCV to be displayed full screen\.

  1. Click **Apply**\.

**Exiting full screen on multiple monitors**  
After you extend the displays or enter full screen mode, a tab appears at the top\-center edge of the screen\. To exit full screen mode, choose the tab and then select **Exit fullscreen**\.

**Note**  
By default, DCV will save your display settings\. If DCV detects a different monitor configuration, the display settings will be reset\.