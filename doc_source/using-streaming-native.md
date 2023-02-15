# Streaming modes on Windows, Linux, and macOS clients<a name="using-streaming-native"></a>

To change the streaming mode on Windows, Linux, and macOS clients:

1. In the client, choose **Settings**, **Streaming Mode**\.  
![\[Settings button located in the top-left corner of the interface.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/streaming.png)

1. In the Streaming Mode window, choose one of the following options:
   + **Best responsiveness** — This option prioritizes faster response times\. It might result in lower image quality\.
   + **Best quality** — This option prioritizes higher image quality\. It might result in longer response times\.

1. \(Optional\) For information about network performance, choose **Display Streaming Metrics**\. For more information, see [Streaming metrics](#using-streaming-metrics-native)\.

1. Close the **Streaming Mode** window\.

## Streaming metrics<a name="using-streaming-metrics-native"></a>

The streaming metrics can be used to evaluate your network performance and determine which streaming mode is suitable for your network conditions\. To view the streaming metrics, choose **Settings**, **Streaming Mode**, **Display Streaming Metrics**\.

The streaming metrics provide the following real\-time information:

**Note**  
Metrics are displayed for the current NICE DCV session connection\.
+ **Framerate**—Indicates the number of frames received from the NICE DCV server every second\.
+ **Network latency**—Indicates the amount of time \(in milliseconds\) it takes for a packet of data to be sent to the NICE DCV server and back to the client\.
+ **Bandwidth usage**—Indicates the amount of data being sent and received over the network connection\. The red line shows the peak network throughput\. The yellow line shows the average throughput\. The blue line shows the current \(real\-time\) throughput\. 

The following image shows example streaming metric data\.

![\[example streaming metric data.\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/metrics.png)