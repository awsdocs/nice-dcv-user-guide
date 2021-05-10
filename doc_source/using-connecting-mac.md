# Connecting to a NICE DCV Session Using the macOS Client<a name="using-connecting-mac"></a>

**To connect to a session using the macOS client**

1. Launch the macOS client\.

   If you get an error stating that the application cannot be opened because it is from an unidentified developer, see the [Safely open apps on your Mac](https://support.apple.com/en-ie/HT202491) webpage\.

1. Choose **Connections Settings**, configure your proxy settings as follows, and then choose **Apply**\.
   + To avoid connecting through a proxy, choose **Connect directly**\.
   + To connect to the NICE DCV server using your preconfigured operating system proxy settings, choose **Use system proxy**\.
   + To connect to the NICE DCV server through a specific HTTP proxy server, choose **Get through web proxy \(HTTP\)**\. Specify the proxy server's host name or IP address, and communication port\. If the HTTP proxy server requires authentication, select the **Proxy server requiring password** check box and enter your user name and password\.
   + To connect to the NICE DCV server through a specific HTTPS proxy server, choose **Get through web proxy \(HTTPS\)**\. Specify the proxy server's host name or IP address, and communication port\. If the web proxy server requires authentication, select the **Proxy server requiring password** check box and enter your user name and password\.
   + To select the transport protocol to use for data transport, choose the **Protocol** tab\. By default, the client is set to automatically use the QUIC protocol \(based on UDP\) for data transport if it is available\. If it is not available, the client uses the WebSocket protocol \(based on TCP\), which is always available\.

     QUIC is available only if the NICE DCV server is configured to support it, and if your network configuration supports UDP communication between the NICE DCV client and the NICE DCV server\. Additionally, it is only supported for direct client\-server communication where there are no intermediate proxies, gateways, or load balancers\.

     You can force the client to use a data transport protocol by explicitly selecting it\. To verify which protocol is in use, check the Streaming Modes dialog\. Additionally, if the QUIC protocol is in use, "QUIC" appears in the titlebar\.

     For more information, see [ Enable the QUIC UDP transport protocol](https://docs.aws.amazon.com/dcv/latest/adminguide/enable-quic.html) in the *NICE DCV Administrator Guide*\.

1. Specify the session details in the following format:

   ```
   server_hostname_or_IP:port#session_id
   ```

   For example, the following connects to a session named `my-session`, which is hosted on a NICE DCV server with the host name `my-dcv-server.com`, over port `8443`:

   ```
   my-dcv-server.com:8443#my-session
   ```

1. Choose **Connect**\.

1. Enter your user name and password and choose **Login**\.
**Note**  
By default, the connection is terminated after three unsuccessful login attempts\. To try again, restart the connection\.

1. If you are prompted to verify the server's certificate, confirm the certificate's fingerprint with your NICE DCV administrator\. If the fingerprint is valid, choose **Trust**\.