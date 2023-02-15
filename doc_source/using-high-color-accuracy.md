# Using high color accuracy<a name="using-high-color-accuracy"></a>

By default, NICE DCV uses YUV 4:2:0 chroma subsampling when compressing the display output and then updates the parts of the screen that are not changing over time to a full lossless RGB implementation\. This default behavior aims to strike a balance between performance and image fidelity, though it may introduce chroma artifacts\. By enabling the High color accuracy setting, the YUV chroma subsampling will be set to 4:4:4, thus increasing color fidelity\. However this will increase network bandwidth and could affect performance of clients, especially at high resolution, because most client machines do not support HW accelerated decoding when using YUV 4:4:4\.

The steps for setting the high color accuracy depend on the client used\.

**Topics**
+ [High color accuracy on native clients](#using-high-color-accuracy-native)
+ [High color accuracy on Web browser client](#using-high-color-accuracy-web)

## High color accuracy on native clients<a name="using-high-color-accuracy-native"></a>

As long as you are using a NICE DCV Server and a NICE DCV Client both having version 2022\.0 or later, please follow these steps to enable high color accuracy:

1. In the client, choose **Settings**, **Streaming Mode**\.  
![\[Settings button located in the top-left corner of the interface.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/windows-yuv444.png)

1. In the Streaming Mode window, the High color accuracy \(YUV 4:4:4\) checkbox allows to enable or disable the corresponding feature\.

1. Close the **Streaming Mode** window\.

## High color accuracy on Web browser client<a name="using-high-color-accuracy-web"></a>

In order to use high color accuracy on Web browser client you need a NICE DCV Server with version 2022\.0 or later, as well as a browser supporting the [VideoDecoder](https://developer.mozilla.org/en-US/docs/Web/API/VideoDecoder) interface of the Web Codecs API\.

The steps for enabling the high color accuracy are the same across all supported web browsers\.

1. In the client, choose **Session**, **Preferences**\.  
![\[Session is located inside the menu in the top-right of the interface.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/web-preferences-menu.png)

1. Under the **Display** tab, if the high color accuracy feature is available, the corresponding toggle will be visible and allows to specify whether to enable or disable the YUV chroma subsampling set to 4:4:4:  
![\[Display is the second tab from the left inside the Preferences modal.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/web-preferences-yuv444.png)

1. Save and close the **Preferences** modal\.