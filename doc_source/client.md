# NICE DCV clients<a name="client"></a>

NICE DCV offers a Windows client, Linux client, web browser client, and macOS client\. The clients offer similar feature sets, but there are some differences\. Choose the NICE DCV client that meets your specific requirements\.

**Topics**
+ [Requirements](#requirements)
+ [Supported features](#client-features)
+ [Windows client](client-windows.md)
+ [Web browser client](client-web.md)
+ [Linux client](client-linux.md)
+ [macOS client](client-mac.md)

## Requirements<a name="requirements"></a>

To use NICE DCV, ensure that the client computers meet the following minimum requirements\. Bear in mind that your experience is dependent on the number of pixels that are streamed from the NICE DCV server to the NICE DCV client\.


|  | Windows client | Web browser client | Linux client | macOS client | 
| --- | --- | --- | --- | --- | 
| **Software** |  The Windows client is supported on 32\-bit and 64\-bit versions of the following operating systems: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/userguide/client.html) The client requires the following additional software: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/userguide/client.html)  |  The web browser client is supported on the latest three major versions of the following browsers, across all major desktop operating systems \(Windows, macOS, and Linux\): [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/userguide/client.html) The web browser client also requires WebGL and asm\.js\. The web browser client isn't supported on mobile operating systems, such as Android and iOS\.  |  The Linux client is supported on the following modern Linux operating systems: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/userguide/client.html)  |  macOS clients with Intel processors require macOS Mojave \(10\.14\) or later\. macOS clients with Apple M1 processors require macOS Big Sur \(11\)\.  | 
| **Network** | The client must connect to the NICE DCV server, and it must communicate over the required port\. By default, this is port 8443\. | 

For more information about the NICE DCV server requirements, see [ NICE DCV server requirements](https://docs.aws.amazon.com/dcv/latest/adminguide/servers.html#requirements) in the *NICE DCV Administrator Guide*\.

## Supported features<a name="client-features"></a>

The following table compares the features that are supported by the NICE DCV clients\.


| Feature | [Windows client](client-windows.md) | [Web browser client](client-web.md) | [Linux client](client-linux.md) | [macOS client](client-mac.md) | 
| --- | --- | --- | --- | --- | 
|  [Connect to Windows NICE DCV servers](using-connecting.md)  | ✓ | ✓ | ✓ | ✓ | 
|  [Connect to Linux NICE DCV servers](using-connecting.md)  | ✓ | ✓ | ✓ | ✓ | 
|  [QUIC UDP transport protocol](using-connecting.md)  | ✓ | ✗ | ✓ | ✓ | 
|  [Manage streaming modes](using-streaming.md)  | ✓ | ✓ | ✓ | ✓ | 
|  [Transfer files](using-transfer.md)  | ✓ | ✓ | ✓ | ✓ | 
|  [Print from sessions](using-print.md)  | ✓ | ✓1 | ✓ | ✓ | 
|  [Copy and paste](using-copy-paste.md)  | ✓ | ✓ | ✓ | ✓ | 
|  [Smart card support](using-smartcard.md)  | ✓ | ✗ | ✓ | ✓ | 
|  [USB remotization support](using-usb.md)  | ✓ \(installable client\) | ✗ | ✗ | ✗ | 
|  [Connection file support](using-connection-file.md)  | ✓ | ✗ | ✓ | ✓ | 
|  Stereo 2\.0 audio playback  | ✓ | ✓ | ✓ | ✓ | 
|  Surround sound audio playback  | ✓ \(up to 7\.1\) | ✗ | ✓ \(up to 5\.1\) | ✗ | 
|  Stereo 2\.0 audio recording  | ✓ | ✓ | ✓ | ✓ | 
|  Touchscreen support  | ✓ \(Windows 8\.1 and later\) | ✓ 2 | ✓ | ✗ | 
|  Stylus support  | ✓ \(Windows 10 and later\) | ✓ 3 | ✓ | ✓ | 
|  Gamepad support  | ✓ \(Windows 10 and later\) | ✗ | ✗ | ✗ | 
|  [Multiple monitor support](using-multiple-screens.md)  | ✓ | ✓4 | ✓ | ✓ | 
|  [Extending full screen across selected monitors](using-multiple-screens.md)  | ✓ | ✗ | ✗ | ✗ | 
|  [Webcam support](using-webcam.md)  | ✓ | ✓ 5 | ✓ | ✓ | 
|  [Setting time zone](setting-timezone.md)  | ✓ | ✓ | ✓ | ✓ | 
|  [Using accurate audio/video synchronization](using-av-sync.md)  | ✓ | ✗ | ✓ | ✓ | 

1These clients support printing to a file only\. They don't support printing to a local printer\.

2 Supported by Firefox, Edge, and Google Chrome\.

3 Supported in Chromium\-based browsers only\. This includes Google Chrome and Microsoft Edge version 79 and later\. Tilt and pressure events aren't supported in other browsers\.

4Support for up to two monitors\.

5Supported in Chromium\-based browsers only\. This includes Google Chrome and Microsoft Edge version 79 and later\. This doesn't include Firefox and Safari\.

For more information about the NICE DCV server features, see [ NICE DCV server features](https://docs.aws.amazon.com/dcv/latest/adminguide/servers.html#features) in the *NICE DCV Administrator Guide*\.