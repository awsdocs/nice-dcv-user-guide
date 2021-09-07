# Windows Client<a name="client-windows"></a>

The NICE DCV Windows client is supported on Windows computers only\. The Windows client is a standalone application that runs natively on the Windows operating system\.

For more information about connecting to a NICE DCV session using the Windows client, see [Connecting to a NICE DCV session using the Windows client](using-connecting-win.md)\.

The Windows client is available in two versions: an installable version and a portable version\. Both versions have the same minimum system requirements and have the same features\.

**Contents**
+ [Installable Windows Client](#client-windows-install)
+ [Portable Windows Client](#client-windows-portable)

## Installable Windows Client<a name="client-windows-install"></a>



You can use an installation wizard to install the client\. The wizard takes you through a series of steps where you can customize your client installation\. Or, you can use the command line to perform an unattended installation\. This second method uses default settings to automate the installation procedure\.

Before using the wizard or the command line to install the client, make sure that your computer has the required software\. For a complete list of required software, see [Requirements](client.md#requirements)\.

**To install the Windows client using the installation wizard**

1. Download the [Windows client installer](https://d1uj6qtbmh3dt5.cloudfront.net/2021.2/Clients/nice-dcv-client-Release-2021.2-7774.msi)\.

1. Run the installer\.

1. On the **Welcome** screen, choose **Next**\.

1. On the **End\-User License Agreement** screen, read the license agreement\. If you accept the terms, select the **I accept the terms in the License Agreement** check box\. Choose **Next**\.

1. On the **Destination Folder** screen, choose **Next** to keep the default installation folder\. To install the client in a different folder, change the destination path, and then choose **Next**\.

1. \(Optional\) On the **Drivers Selection** screen, select **USB device remotization** and choose **Will be installed on local hard drive**, **Next**\. This installs the drivers required to support some specialized USB devices\. These devices include 3D pointing devices and graphic tablets\.
**Note**  
Using specialized USB devices requires additional client and server configuration\. For instructions, see [Using USB remotization](using-usb.md)\.

1. On the **Ready to install** screen, choose **Install**\.

**To install the Windows client using an unattended installation**

1. Download the [Windows client installer](https://d1uj6qtbmh3dt5.cloudfront.net/2021.2/Clients/nice-dcv-client-Release-2021.2-7774.msi)\.

1. Open a command prompt window and navigate to the folder where you downloaded the installer\.

1. Run the unattended installer\.

   ```
   C:\> msiexec.exe /i nice-dcv-client-Release-2021.2-7774.msi /quiet /norestart /l*v dcv_client_install_msi.log
   ```

   To install all of the optional components, including the USB driver, include the `ADDLOCAL=ALL` option in the command\.

   ```
   C:\>  msiexec.exe /i nice-dcv-client-Release-2021.2-7774.msi ADDLOCAL=ALL /quiet /norestart /l*v dcv_client_install_msi.log
   ```

## Portable Windows Client<a name="client-windows-portable"></a>

The Windows client is also available in a portable version\. You don't need to install the portable version on your computer\. In fact, you can copy it to a USB drive and run it directly from the USB drive on any Windows computer that meets the minimum requirements\.

**To use the portable Windows client**

1. Download the portable [Windows client zip file](https://d1uj6qtbmh3dt5.cloudfront.net/2021.2/Clients/nice-dcv-client-Release-portable-2021.2-7774.zip)\.

1. Extract the contents of the zip file\.

1. To launch the client, open the extracted folder, navigate to `/bin/`, and double\-click `dcvviewer.exe`\.