# Web browser client<a name="client-web"></a>

The NICE DCV web browser client runs inside a web browser\. You don't need to install the web client\. The web browser client is supported on the following browsers across all major desktop operating systems \(including Windows, macOS, and Linux\):


| Browser | Version | 
| --- | --- | 
| Google Chrome | Latest three major versions | 
| Mozilla Firefox | Latest three major versions | 
| Microsoft Edge | Latest three major versions | 
| Apple Safari | Latest three major versions | 

For instructions on how to connect to a NICE DCV session using the web browser client, see [Connecting to a NICE DCV session using the web browser client](using-connecting-browser-connect.md)\.

**WebCodecs**  
The web browser client can use WebCodecs to use video decoders that are already present in the browser\. This can improve frame rate, because packets can be decoded by components of the browser\. The NICE DCV web browser client will automatically use it if supported by the browser\.

The use of WebCodecs is available on the following browsers:
+ Google Chrome version 94 and later
+ Microsoft Edge version 94 and later

All major operating systems are supported\. This includes Windows, macOS, and Linux\.

**Limitations**  
The web browser client has the following limitations:
+ It supports up to two screens with a maximum resolution of 1920x1080\. The maximum resolution can be overriden on the server side\. For more information, see [Managing the NICE DCV Session Display Layout](https://docs.aws.amazon.com/dcv/latest/adminguide/managing-session-display.html) in the *NICE DCV Administrator Guide*\.
+ It uses the web browser's proxy configuration\.