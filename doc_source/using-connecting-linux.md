# Connecting to a NICE DCV session using the Linux client<a name="using-connecting-linux"></a>

The steps for connecting to a NICE DCV session are the same across all Linux clients\.

**To connect to a session using the Linux client**

1. Launch the Linux client\.

1. Choose **Connections Settings**, configure your proxy settings as follows, and then choose **Apply**\.
   + To avoid connecting through a proxy, choose **Connect directly**\.
   + To connect to the NICE DCV server using your preconfigured operating system proxy settings, choose **Use system proxy**\.
   + To connect to the NICE DCV server through a specific HTTP proxy server, choose **Get through web proxy \(HTTP\)**\. Specify the IP address or the hostname of the proxy server as well as the communication port\. If the HTTP proxy server requires authentication, select the **Proxy server requiring password** check box and enter your user name and password\.
   + To connect to the NICE DCV server through a specific HTTPS proxy server, choose **Get through web proxy \(HTTPS\)**\. Specify the IP address or the hostname of the proxy server as well as the communication port\. If the web proxy server requires authentication, select the **Proxy server requiring password** check box and enter your user name and password\.
   + To select the transport protocol to use for data transport, choose the **Protocol** tab\. By default, the client uses the QUIC protocol \(based on UDP\) for data transport if it's available\. If it isn't available, the client uses the WebSocket protocol \(based on TCP\)\. This option is always available\.

     QUIC is available only if the following two conditions are met\. First, the NICE DCV server is configured to support it\. Second, your network configuration supports UDP communication between the NICE DCV client and the NICE DCV server\. Additionally, it's only supported for direct client\-server communication where there are no intermediate proxies, gateways, or load balancers\.

     You can force the client to use a data transport protocol by explicitly selecting it\. To verify which protocol is in use, check the Streaming Modes dialog\. Additionally, if the QUIC protocol is in use, "QUIC" appears in the titlebar\.

     For more information and instructions, see [ Enable the QUIC UDP transport protocol](https://docs.aws.amazon.com/dcv/latest/adminguide/enable-quic.html) in the *NICE DCV Administrator Guide*\.

1. Specify the session details in the following format:

   ```
   server_hostname_or_IP:port#session_id
   ```

   In the following example, the command connects to a session that's named `my-session`\. This session is hosted on a NICE DCV server with the hostname `my-dcv-server.com`\. It's connected over port `8443`\.

   ```
   my-dcv-server.com:8443#my-session
   ```

1. Choose **Connect**\.

1. Enter your user name and password and choose **Login**\.
**Note**  
By default, the connection is terminated after three unsuccessful login attempts\. To try again, restart the connection\.

1. If you are prompted to verify the certificate on the server, confirm the fingerprint of the certificate with your NICE DCV administrator\. If the fingerprint is valid, choose **Trust & Connect**\.