# Getting Started with NICE DCV<a name="getting-started"></a>

NICE Desktop Cloud Visualization is a remote visualization technology that enables users to securely connect to graphic\-intensive 3D applications hosted on a remote high\-performance server\. With NICE DCV, you can make a server's high\-performance graphics processing capabilities available to multiple remote users by creating secure client sessions\. This enables your users to use resource\-intensive applications with relatively low\-end client computers by using the server's processor, GPU, I/O capabilities, and memory\.

In a typical NICE DCV scenario, a graphic\-intensive application, such as a 3D modeling or computer\-aided design application, is hosted on a high\-performance server that provides a high\-end GPU, fast I/O capabilities, and large amounts of memory\. The **NICE DCV server** software is installed and configured on the server and it is used to create a secure session\. You use a **NICE DCV client** to remotely connect to the session and use the application hosted on the server\. The server uses its hardware to perform the high\-performance processing required by the hosted application\. The **NICE DCV server** software compresses the visual output of the hosted application and streams it back to you as an encrypted pixel stream\. Your **NICE DCV client** receives the compressed pixel stream, decrypts it, and then outputs it to your local display\.

**Contents**
+ [Step 1: Get the Session Information](#getting-started-session)
+ [Step 2: Choose a Client](#getting-started-choose)

## Step 1: Get the NICE DCV Session Information<a name="getting-started-session"></a>

After the NICE DCV session is running on the NICE DCV server, you must have specific information to be able to connect to it\. Contact your NICE DCV administrator if you do not have the following information:
+ The NICE DCV server's IP address or host name
+ The port over which the NICE DCV server is configured to communicate\. Port 8443 is the default port used by the NICE DCV server\.
+ The session ID
+ A user name and password to connect to the NICE DCV host server

## Step 2: Choose a NICE DCV Client<a name="getting-started-choose"></a>

Next, choose the NICE DCV client that best meets your needs\. NICE DCV offers the following clients: 
+ A native Windows client
+ A web browser client
+ A Linux client

For more information about the available clients, see [NICE DCV Clients](client.md)\.

After you have chosen your preferred NICE DCV client, you can use it to connect to, and interact with the NICE DCV session\. For more information about using the NICE DCV clients to interact with sessions, see [Using NICE DCV](using.md)\.