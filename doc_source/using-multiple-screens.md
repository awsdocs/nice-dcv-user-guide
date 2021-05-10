# Using Multiple Screens<a name="using-multiple-screens"></a>

The NICE DCV clients enable you to extend the session's display across multiple screens\.

With the Windows, Linux, and macOS clients, the extended display matches your physical display layout and screen resolutions\. For example, if you have three screens connected to your local computer, the server extends the session's display across three screens and matches your screen resolutions\.

With the web browser client, the session display can be extended to up to two screens with 1920x1080 screen resolution\. When the display is extended, the additional screen is opened in a new browser window\. The second extends the display to the right of the original screen\. Ensure that you position the screens accordingly\.

You can also manually specify custom display layouts\. For more information, see [ Managing the NICE DCV Session Display Layout](https://docs.aws.amazon.com/dcv/latest/adminguide/managing-session-display.html) in the *NICE DCV Administrator Guide*\.

**Note**  
If the requested layout is not supported by the server, the layout might be adjusted to match the server's display limitations\. If the layout can't be adjusted to match the server's display limitations, the request fails and the changes are not applied\.

**To extend the display**  
Do one of the following depending on your client\.
+ Windows and Linux clients

  In the client, choose **Enter fullscreen**, **Across all monitors**\.  
![\[Fullscreen button located on the native client toolbar.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/native-extend.png)
+ macOS client

  In the client, choose **View**, **Full Screen Current Monitor**\.  
![\[Multiscreen button located on the web browser client toolbar.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/macos-extend.png)
+ Web browser client

  In the client, choose **Multiscreen**\.  
![\[Multiscreen button located on the web browser client toolbar.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/web-extend.png)

After you extend the displays or enter fullscreen mode, a tab appears at the top\-center edge of the screen\. To exit fullscreen mode, click the tab and choose **Exit fullscreen**\.