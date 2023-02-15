# Streaming modes on Web browser client<a name="using-streaming-web"></a>

The steps for managing the streaming modes are the same across all supported web browsers\.

1. In the client, choose **Session**, **Preferences**\.  
![\[Session is located inside the menu in the top-right of the interface.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/web-preferences-menu.png)

1. Under the **Display** tab, choose one of the following options from the **Streaming options** section:
   + **Best responsiveness** — This option prioritizes faster response times\. It might result in lower image quality\.
   + **Best quality** — This option prioritizes higher image quality\. It might result in longer response times\.  
![\[Display is the second tab from the left inside the Preferences modal.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/web-preferences-display.png)

1. \(Optional\) For information about network performance, choose **Display Streaming Metrics**\. For more information, see [Streaming metrics](#using-streaming-metrics-web)\.

1. Save and close the **Preferences** modal\.

## Streaming metrics<a name="using-streaming-metrics-web"></a>

The streaming metrics can be used to evaluate your network performance and determine which streaming mode is suitable for your network conditions\.

The streaming metrics provide the following real\-time information:

**Note**  
Metrics are displayed for the current NICE DCV session connection\.
+ **Framerate**—Indicates the number of frames received from the NICE DCV server every second\.
+ **Network latency**—Indicates the amount of time \(in milliseconds\) it takes for a packet of data to be sent to the NICE DCV server and back to the client\.
+ **Bandwidth usage**—Indicates the amount of data being sent and received over the network connection\. The red line shows the peak network throughput\. The yellow line shows the average throughput\. The blue line shows the current \(real\-time\) throughput\. 

To view the streaming metrics:

1. In the client, choose **Session**, **Preferences**\.  
![\[Session is located inside the menu in the top-right of the interface.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/web-preferences-menu.png)

1. Under the **Display** tab, enable the toggle to show ** Streaming metrics in the toolbar**\.

1. Close the **Preferences** modal\.

1. The streaming metrics are then displayed in the center of the client toolbar\.  
![\[Streaming metrics in the center of the client toolbar.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/web-toolbar-streaming-metrics.png)

1. Click on the streaming metrics to see more detailed streaming data like in the following example\.  
![\[Streaming metrics data example\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/web-streaming-metrics-data.png)

1. \(Optional\) Close the **Metrics** modal\.