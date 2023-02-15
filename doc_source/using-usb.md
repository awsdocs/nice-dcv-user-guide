# Using USB remotization<a name="using-usb"></a>

NICE DCV allows you to use specialized USB devices, such as 3D pointing devices and two\-factor authentication USB dongles\. These devices must be physically connected to your computer to interact with an application that's running on a NICE DCV server\.

Graphic tablets, gamepads, and smart card readers are automatically supported by NICE DCV and do not require USB remotization to be used\.

You must be authorized to use this feature\. If you are not authorized, the functionality is not available in the client\. For more information, see [Configuring NICE DCV Authorization](https://docs.aws.amazon.com/dcv/latest/adminguide/security-authorization.html) in the *NICE DCV Administrator Guide*\.

**Note**  
USB remotization is only supported in the installable Windows client\. It isn't supported by the portable Windows client, web browser client, Linux client, or macOS client\. Additional configuration might be required on the NICE DCV server\. For more information and instructions, see [Enabling USB Remotization](https://docs.aws.amazon.com/dcv/latest/adminguide/manage-usb-remote.html) in the *NICE DCV Administrator Guide*\.

By default, the most commonly used USB devices are supported\. For these devices, you can connect them to your computer and use them on the server without any additional configuration required\. To use a USB device, connect it to your computer\. In the client, choose **Settings**, and then move the slider next to the USB device in the list\.

However, some specialized USB devices aren't supported in the default configuration\. Unsupported devices don't appear in the **Settings** menu after they're connected\. These devices must be added to the USB device *allow list* on the NICE DCV server before they can be used\. After they're added to the allow list, they appear in the **Settings** menu in the client\.

**To use a device that must be added to the allow list on the NICE DCV server**

1. Ensure that you installed the latest version of the Windows client and that you opted to install the USB remotization drivers\. For more information, see [Installable Windows client](client-windows.md#client-windows-install)\.

1. Ensure that the USB device is connected to your computer and that you installed the required hardware drivers\.

1. Navigate to `C:\Program Files (x86)\NICE\DCV\Client\bin\` and run `dcvusblist.exe`\.

1. Open the context \(right\-click\) menu for the USB device in the list and choose **Copy filter string**\. Then, send the filter string to your NICE DCV server administrator\.
**Note**  
The NICE DCV server administrator adds the filter string for each USB device to the allow list\. For more information, see [Enabling USB Remotization](https://docs.aws.amazon.com/dcv/latest/adminguide/manage-usb-remote.html) in the *NICE DCV Administrator Guide*\.

1. After the device is added to the allow list on the NICE DCV server, choose **Settings**\. Then, move the slider next to the USB device to use it\.