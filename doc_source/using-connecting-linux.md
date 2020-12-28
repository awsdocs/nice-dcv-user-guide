# Connecting to a NICE DCV Session Using the Linux Client<a name="using-connecting-linux"></a>

The steps for connecting to a NICE DCV session are the same across all Linux clients\.

**To connect to a session using the Linux client**

1. Launch the Linux client\.

1. Choose **Connections Settings**, configure your proxy settings as follows, and then choose **Apply**\.
   + To avoid connecting through a proxy, choose **Connect directly**\.
   + To connect to the NICE DCV server using your preconfigured operating system proxy settings, choose **Use system proxy**\.
   + To connect to the NICE DCV server through a specific HTTP proxy server, choose **Get through web proxy \(HTTP\)**\. Specify the proxy server's hostname or IP address, and communication port\. If the HTTP proxy server requires authentication, select the **Proxy server requiring password** check box and enter your user name and password\.
   + To connect to the NICE DCV server through a specific HTTPS proxy server, choose **Get through web proxy \(HTTPS\)**\. Specify the proxy server's hostname or IP address, and communication port\. If the web proxy server requires authentication, select the **Proxy server requiring password** check box and enter your user name and password\.
   + To use the QUIC transport protocol \(which is based on UDP\) for data transport, choose the **Advanced** tab, and then choose **QUIC \(with Datagram Extension**\)\.

     If you choose QUIC, authentication traffic is still transported over the WebSocket \(TCP\) port\. By default, both QUIC and WebSocket traffic is transported over port 8443\. If your administrator configured the NICE DCV server to use different ports, specify the ports to use\.

     You can only use QUIC if it has been enabled on the server\. For more information, see [ Enable the QUIC UDP transport protocol](https://docs.aws.amazon.com/dcv/latest/adminguide/enable-quic.html) in the *NICE DCV Administrator Guide*\.

1. Specify the session details in the following format:

   ```
   server_hostname_or_IP:port#session_id
   ```

   For example, the following connects to a session named `my-session`, which is hosted on a NICE DCV server with the hostname `my-dcv-server.com`, over port `8443`:

   ```
   my-dcv-server.com:8443#my-session
   ```

1. Choose **Connect**\.

1. Enter your user name and password and choose **Login**\.
**Note**  
By default, the connection is terminated after three unsuccessful login attempts\. To try again, restart the connection\.

1. If you are prompted to verify the server's certificate, confirm the certificate's fingerprint with your NICE DCV administrator\. If the fingerprint is valid, choose **Trust**\.