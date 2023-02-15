# Pushing metrics to external monitoring tools<a name="pushing-metrics"></a>

EnginFrame can push its metrics to external monitoring tools through StatsD\. StatsD is a network daemon that runs on the [Node\.js](http://nodejs.org) platform and listens for statistics that are provided by tools such as counters and timers\. StatsD sends aggregates to one or more pluggable backend services, such as [Amazon™ CloudWatch](https://aws.amazon.com/cloudwatch/)\.

## Supported monitoring tools<a name="pushing-metrics.supported-tools"></a>

We support every monitoring tool that implements the StatsD backend service to forward metrics\. For more information about available StatsD backend services, see [Supported Backends](https://github.com/statsd/statsd/blob/master/docs/backend.md#supported-backends) in the *StatsD README* on the GitHub website\.

## Prerequisites<a name="pushing-metrics.prerequisites"></a>

The following are required to configure EnginFrame to use StatsD to push metrics to an external monitoring tool\. 
+ A monitoring tool that StatsD supports\.
+ A running StatsD instance that's configured to forward metrics to the monitoring tools in use\. StatsD must be configured to use User Datagram Protocol \(UDP\)\. This is the default option\. For more information about configuring StatsD, see [Installation and Configuration](https://github.com/statsd/statsd#installation-and-configuration) in the *StatsD README* on the GitHub website\.

## Configuration<a name="pushing-metrics.configuration"></a>

To configure EnginFrame to push metrics to a StatsD instance, you must configure the `STATSD_ADDR` and `STATSD_PORT` variables\. These are located in the following configuration file: `$EF_ROOT/plugins/admin/conf/admin.statistics.efconf`\.

In the following example configuration, StatsD is run locally on port 8125\.

```
##########################################################################
# StatsD Server Configuration
##########################################################################

STATSD_ADDR=localhost
STATSD_PORT=8125
```

## Troubleshooting<a name="pushing-metrics.troubleshooting"></a>

EnginFrame provides the `$EF_LOGDIR/admin.log` log file\. You can use it to troubleshoot and diagnose errors\.