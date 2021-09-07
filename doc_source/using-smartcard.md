# Using a smart card<a name="using-smartcard"></a>

You can use NICE DCV to use one or more smart cards that's connected to your client computer\. You can do this using the standard Personal Computer/Smart Card \(PC/SC\) interface, in a NICE DCV session\. For each session, only one connected client can connect a smart card at a time\. This is especially important in environments where multiple clients connect to the same session\.

Smart card access is supported with the Windows, Linux, and macOS clients only\. It's not supported with the web browser client\.

You must be authorized to use this feature\. If you are not authorized, the functionality is not available in the client\. For more information, see [Configuring NICE DCV Authorization](https://docs.aws.amazon.com/dcv/latest/adminguide/security-authorization.html) in the *NICE DCV Administrator Guide*\.

**To use a smart card**

1. Launch the client and connect to the NICE DCV session\.

1. Connect the smart card to the session or release it\.

   While your smart card is connected, no other clients who are connected to the session can connect a smart card\. This is because only one client can connect a smart card at a time\.

   After you're done using the smart card in the DCV session, release it\. After it's released, other clients who are connected to the session can connect a smart card\. The smart card is automatically released when you disconnect from the session\.

   1. In the client, choose **Settings**, **Removable Devices**\.

   1. To connect a smart card, enable the **Smart Card** toggle\. To release control of the smart card, disable the **Smart Card** toggle\.  
![\[Settings button located in the top-left corner of the interface.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/smartcard.png)

1. \(Optional\) To have the NICE DCV server cache smart card data, enable the smart card caching feature\. By default, smart card caching is disabled\. With smart card caching enabled, the server caches the results of recent calls to the client's smart card\. This helps to reduce the amount of traffic that is transferred between the client and the server and improves performance\.

   You can't enable smart card caching if it's permanently disabled on the server\. For more information, see [Configuring Smart Card Caching](https://docs.aws.amazon.com/dcv/latest/adminguide/manage-smart-card.html) in the *NICE DCV Administrator Guide*\. 

   To enable smart card caching, set and export the `DCV_PCSC_ENABLE_CACHE` environment variable\. In the session, open a terminal window and run the following command:
   + Windows server

     To enable smart card caching for the current terminal window, run the following command\.

     ```
     C:\> set DCV_PCSC_ENABLE_CACHE=1
     ```

     To enable smart card caching permanently for all applications on the server, run the following command\.

     ```
     C:\> setx DCV_PCSC_ENABLE_CACHE 1
     ```
   + Linux server

     ```
     $  export DCV_PCSC_ENABLE_CACHE=1
     ```
**Note**  
Make sure to run the following command in the same terminal that you intend to launch the application from \(in step 4\)\.

1. \(Linux NICE DCV server only\) Launch the required application with smart card support\. In the session, open a terminal window, and launch the application using the `dcvscrun` command\. For example, to launch `firefox` with smart card support, use the following command:

   ```
   $  dcvscrun firefox
   ```
**Important**  
If you enabled smart card caching, run the following command in the same terminal that you set and exported the `DCV_PCSC_ENABLE_CACHE` environment variable in\.