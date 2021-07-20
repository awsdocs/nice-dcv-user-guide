# Printing<a name="using-print"></a>

NICE DCV enables you to print content from a NICE DCV session hosted on a Windows NICE DCV server only\. The available printing devices depend on the client you're using\.
+ **Windows client** — You can print to the physical printer connected to your client computer, or you can print to a `.PDF` document using the NICE DCV virtual printer\.
+ **Linux client** and **macOS client** — You can print to a `.PDF` document using the NICE DCV virtual printer\.
+ **Web browser client**
  + Google Chrome, Mozilla Firefox, or Apple Safari — You can print to a `.PDF` document using the NICE DCV virtual printer\.
  + Microsoft Edge or Internet Explorer — You can print to a `.XPS` document using the NICE DCV virtual printer\.

When you print to the NICE DCV virtual printer, the content is exported to a printable file\. You can download it to your local computer using the client and then print it using your local printer\.

You must be authorized to use this feature\. If you are not authorized, the functionality is not available in the client\. For more information, see [Configuring NICE DCV Authorization](https://docs.aws.amazon.com/dcv/latest/adminguide/security-authorization.html) in the *NICE DCV Administrator Guide*\.

**To print content from the session**

1. In the client, open the Print window\.

1. In the Print window, choose one of the following printing devices and then choose **Print**\.
   + \(All clients connected to all Windows and Linux server\) **DCV Printer** — Prints to the NICE DCV virtual printer
   + \(Windows client connected to Windows server only\) ***<local\-printer\-name>*\-DCV Redirected** — Prints to the local printer
   + \(Windows client connected to Linux server only\) ***<local\-printer\-name>*\-DCV\-Redirected\-*<connection\-id>*** — Prints to the local printer

1. If you print to the NICE DCV virtual printer, a notification appears when the file is ready for download\. In the top\-right corner, choose **Notifications**, locate the Print notification in the list, and then choose **Download**\.
   + If you are using the web browser client, after the download has completed, choose **Show in folder**\.
   + If you are using the Windows client, the printer dialog is automatically opened when the file is downloaded\.
   + If you are using the Linux or macOS clients, the downloaded file is automatically opened with the default associated application\.
**Note**  
The file is deleted from the NICE DCV server after you have downloaded it, and it is no longer available for download\.