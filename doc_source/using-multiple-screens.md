# Using multiple screens<a name="using-multiple-screens"></a>

You can use the NICE DCV clients to extend the display for a session across multiple screens\.

With the Windows, Linux, and macOS clients, the extended display matches your physical display layout and screen resolutions\. For example, assume that you have three screens connected to your local computer\. In this case, the server extends the display for a session across all three screens and matches the specific screen resolutions of your displays\.

With the web browser client, the session display can be extended to up to two screens with 1920x1080 screen resolution\. When the display is extended, the additional screen is opened in a new browser window\. The second extends the display to the right of the original screen\. Ensure that you position the screens accordingly\.

You can also manually specify custom display layouts\. For more information, see [ Managing the NICE DCV Session Display Layout](https://docs.aws.amazon.com/dcv/latest/adminguide/managing-session-display.html) in the *NICE DCV Administrator Guide*\.

**Note**  
If the requested layout isn't supported by the server, the layout might be adjusted to match the display limits of your server\. If the layout can't be adjusted, the request fails and the changes aren't applied\.

**To extend the display**  
Do one of the following depending on your client\.
+ Windows and Linux clients

  In the client, choose **Enter fullscreen**, **Across all monitors**\.  
![\[Fullscreen button that's located on the native client toolbar.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/native-extend.png)
+ macOS client

  In the client, choose **View**, **Full Screen Current Monitor**\.  
![\[Multiscreen button that's located on the web browser client toolbar.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/macos-extend.png)
+ Web browser client

  In the client, choose **Multiscreen**\.  
![\[Multiscreen button that's located on the web browser client toolbar.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/web-extend.png)

After you extend the displays or enter fullscreen mode, a tab appears at the top\-center edge of the screen\. To exit fullscreen mode, choose the tab and then **Exit fullscreen**\.