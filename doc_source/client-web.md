# Web browser client<a name="client-web"></a>

The NICE DCV web browser client runs inside a web browser\. You don't need to install the web client\. The web browser client is supported on the following browsers across all major desktop operating systems \(including Windows, macOS, and Linux\):
+ Firefox
+ Chrome
+ Edge
+ Internet Explorer 11
+ Safari 11

For instructions on how to connect to a NICE DCV session using the web browser client, see [Connecting to a NICE DCV session using the web browser](using-connecting-browser-connect.md)\.

**WebCodecs**  
The web browser client can use WebCodecs to use video decoders that are already present in the browser\. This can improve frame rate, because packets can be decoded by components of the browser\.

The use of WebCodecs is available on the following browsers:
+ Google Chrome version 86 and later
+ Microsoft Edge version 86 and later
+ Opera version 72 and later

All major operating systems are supported\. This includes Windows, macOS, and Linux\.

**Note**  
WebCodecs is an experimental API and is not standardized\. To use WebCodecs, you must enable experimental features\. Open your browser from the command line by entering the executable file for your browser and the following command to enable WebCodecs on your browser:  
`browser.exe --enable-blink-features=WebCodecs`  
On Windows, you can enable WebCodecs manually:  
Locate the executable file for your browser in File Explorer\.
Right\-click the file to open the context menu and choose Properties from the context menu\.
Place your curser at the end of the text in the **Target** field and enter the following command:  
`--enable-blink-features=WebCodecs`  

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/webcodecs-properties-update.png)
Choose **OK**\.

**Limitations**  
The web browser client has the following limitations:
+ It supports up to two screens with a maximum resolution of 1920x1080\. The maximum resolution can be overriden on the server side\. For more information, see [Managing the NICE DCV Session Display Layout](https://docs.aws.amazon.com/dcv/latest/adminguide/managing-session-display.html) in the *NICE DCV Administrator Guide*\.
+ It uses the web browser's proxy configuration\.