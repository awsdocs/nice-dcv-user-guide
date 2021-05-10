# Using a Webcam<a name="using-webcam"></a>

NICE DCV enables you to use a webcam connected to your local client computer in a remote application running in a NICE DCV session\. For each session, only one connected client can use a webcam at a time\. This is especially important in environments where multiple clients connect to the same session\. 

Webcam functionality is supported with all NICE DCV clients\. However, with the web browser client, webcam functionality is only supported with Chromium\-based browsers, such as Google Chrome or Microsoft Edge\.

Webcam functionality is supported on Windows NICE DCV servers only\. It is not supported on Linux NICE DCV servers\.

You must be authorized to use this feature\. If you are not authorized, the functionality is not available in the client\. For more information, see [Configuring NICE DCV Authorization](https://docs.aws.amazon.com/dcv/latest/adminguide/security-authorization.html) in the *NICE DCV Administrator Guide*\.

If you have multiple webcams connected to your local client computer, you can select the webcam that you want to use\. The selected camera is used automatically when the webcam is enabled using the webcam toolbar icon\.

**To select the webcam to use**

1. Launch the client and connect to the NICE DCV session\.

1. Do one of the following depending on your browser\.
   + Windows, Linux, and web browser clients

     Choose **Settings**, **Camera** and then select to webcam to use\.  
![\[Webcam menu option\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/menu.png)
   + macOS client

     Choose **Connection**, **Camera Settings** and then select to webcam to use\.  
![\[Webcam menu option\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/mac-menu.png)

**Note**  
The camera menu items appears only if you are authorized to use a webcam in the session\. If you do not see the camera menu items, you might not be authorized to use a webcam\.
If you are using the web browser client, you are prompted to allow camera detection\. Additionally, you can't select a webcam if your web browser's security settings prevent the use of a webcam\.
You can't change the webcam selection while the webcam is in use, or while another client has enabled a webcam in the session\.

**To start using your webcam in a session**  
You must first enable it\. You can use the webcam icon on the toolbar to enable or disable your webcam for use in the session, and to determine its current state\. The webcam icon appears on the toolbar only if:
+ You are authorized to use a webcam\.
+ You have at least one webcam connected to your local computer\.
+ No other users have enabled a webcam for use in the session\.


| Toolbar icon | Description | 
| --- | --- | 
|  ![\[Webcam disabled\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/disabled.png)  |  Your webcam is disabled in the session\. Other clients can enable a webcam for use in the session\. Click the icon to enable your webcam in the session\. If you have not previously selected the webcam to use, the default webcam is used\.  | 
|  ![\[Webcam enabled\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/enabled.png)  |  Your webcam is enabled in the session, but it is not in use\. While your webcam is enabled, no other clients who are connected to the session can use a webcam\. Click the icon to disable your webcam in the session\.  | 
|  ![\[Webcam in use\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/inuse.png)  |  Your webcam is in use by a remote application in the NICE DCV session\. No other clients can enable a webcam while your webcam is in use\. Click the icon to disable your webcam in the session\.  | 

## Troubleshooting<a name="troubleshoot"></a>

**Topics**
+ [Webcam does not work on Windows 10](#win-10)
+ [Client application says that the webcam is in use](#close-app)

### Webcam does not work on Windows 10<a name="win-10"></a>

Windows 10 provides built\-in privacy settings that manage access to the device’s camera\. If you are running Windows 10 on your client computer, these privacy settings might prevent use of the webcam\.

**Note**  
If you are connecting to a Windows 2019 NICE DCV server, you might need to perform these steps on the NICE DCV server as well\.

To modify the privacy settings on your computer, do the following:

1. Choose the search icon on the toolbar\.

1. Enter `Settings` and press **Enter**\.

1. In the left\-hand panel, choose **Camera**\.

1. For **Allow apps to access your camera**, switch the toggle to the **On** position\.

1. You might need to restart your computer for the changes to take effect\.

### Client application says that the webcam is in use<a name="close-app"></a>

Only one application can use the webcam at a time\. If you are using the webcam in multiple applications, first close the applications where it is no longer needed\.