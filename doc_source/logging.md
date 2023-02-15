# Customizing logging<a name="logging"></a>

Logging is an integral component to any software development project\. During the development stages it offers a valuable source of debugging information for the developer\. During deployment it can provide valuable operational data that allows administrators to diagnose problems as they arise\.

## Tomcat® logging<a name="section-logging-tomcat"></a>

EnginFrame comes with Apache Tomcat® servlet container\. Tomcat® log files are the first source of information concerning EnginFrame's status\. Log files are located on EnginFrame Server's host under `$EF_TOP/logs/<HOSTNAME>/tomcat`\.

These are the most interesting log files:
+ `catalina.out`

  Contains Tomcat®'s Java™ process standard output and standard error\. Tomcat® startup and shutdown messages are written here\.
+ `catalina.[yyyy]-[mm]-[dd].log`

  Contains Tomcat®'s and its libraries logging information on a day\-by\-day basis\. 
+ `localhost_access_log.[yyyy]-[mm]-[dd].txt`

  Contains all web accesses on a day\-by\-day basis\. Any resource served by Tomcat is logged here with information about the amount of transferred data\. Also HTTP status codes like `404 Not Found`, `403 Forbidden` are logged here\. 
+ `enginframe.[yyyy]-[mm]-[dd].log`

  Contains Tomcat®'s error logs about EnginFrame Portal not caught by EnginFrame itself\. 

The standard Tomcat® configuration fits the most common installations\. In case of specific needs you can modify the default `$EF_TOP/<VERSION>/enginframe/conf/logging.properties` configuration\. Refer to the official [Tomcat® documentation](https://tomcat.apache.org/tomcat-9.0-doc/logging.html) fore more details\. 

## EnginFrame server and agent logging<a name="section-logging-server-agent"></a>

**Topics**
+ [Configuration files](#section-logging-server-agent-logfiles)
+ [Apache® Log4j2 log configuration](#section-log4j2-logging)
+ [Change log file locations](#section-logging-server-agent-file-location)
+ [Change log file size and the rotation policy](#section-logging-server-agent-file-rotation)
+ [Change log level](#section-logging-server-agent-verboseness)
+ [Fine tune logging](#section-logging-configuration-fine-tune)

### Configuration files<a name="section-logging-server-agent-logfiles"></a>

The default logging configurations are located under `$EF_TOP/<VERSION>/enginframe/conf`:
+ `log.server.xconf`

  Contains server's configuration\.
+ `log.agent.xconf`

  Contains agent's configuration\.

Both are XML files with the same syntax\.

In case you need to modify the defaults, you can specify a new configuration in the `log.server.xconf` and `log.agent.xconf` files under the configuration directory `$EF_TOP/conf/enginframe`\.

In these files you can configure the location where you store log files, their verbosity level, and rotation policies\. By default, EnginFrame is configured to write only warning and error messages and to keep a history of 4 log files with a 10 MB maximum size\.

The log's default location is under `$EF_TOP/logs/<HOSTNAME>` on server and agent hosts:
+ `ef.log`

  Contains the server's logging\. It also contains the local agent's logs\. It is located on server's host\.
+ `agent.remote.stdout`

  Contains the agent's process standard output\. It is located on the agent's host\.
+ `agent.remote.stderr`

  Contains the agent's process standard error\. It is located on the agent's host\.
+ `agent.remote.log`

  Contains the agent's process logging\. It is located on the agent's host\.

If you need to quickly switch the log configuration to produce verbose logging, you can use `log.server.verbose.xconf` and `log.agent.verbose.xconf` files located in `$EF_TOP/<VERSION>/engifnrame/conf`\.

You need to backup the previous `log.server.xconf` and `log.agent.xconf` files and replace them with the verbose configurations\.

We don't recommend you use a verbose logging configuration when you're in a production environment\. The performance impact of logging can be significant, depending on the logging threshold that is configured and especially if a large number of users are accessing the portal\. 

### Apache® Log4j2 log configuration<a name="section-log4j2-logging"></a>

EnginFrame is configured for Apache® Log4j2 logging as described in the following paragraphs\.

EnginFrame server Log4j2 logging is configured in `${EF_TOP}/<VERSION>/enginframe/conf/log4j2.server.xml`\. By default, logs are written to `${EF_LOGDIR}/ef.log`\.

EnginFrame agent Log4j2 logging is configured in `${EF_TOP}/<VERSION>/enginframe/conf/log4j2.agent.xml`\. By default\. logs are written to `${EF_LOGDIR}/agent.remote.log`\.

Log4j2 log configuration files apply to any EnginFrame internal dependency that uses Log4j2 logging, such as MyBatis or Quartz\.

If you need to modify the defaults, you can specify a new configuration in the `log4j2.server.xml` and `log4j2.agent.xml` files under the configuration directory `$EF_TOP/conf/enginframe`\.

### Change log file locations<a name="section-logging-server-agent-file-location"></a>

The EnginFrame logging system gives you complete flexibility on where to store log files\. For example you may want to move log files from their default location to store them on a high speed file\-system or to conform to your company's policies\. 

The location configuration is done in the `<targets>` section by setting the `<filename>` tag\. The text inside this tag represents the path to the log file\.

For example this XML text sets `${EF_LOGDIR}/ef.log` for the core components: 

```
<targets>
  <enginframe id="core">
    <filename>${EF_LOGDIR}/ef.log</filename>
    ...
```

You can also decide whether to append or overwrite existing files by using the `<append>` tag\. 

In the following example the log file will be overwritten on every server restart: 

```
<targets>
  <enginframe id="core">
    <filename>${EF_LOGDIR}/ef.log</filename>
    <append>false</append>
    ...
```

### Change log file size and the rotation policy<a name="section-logging-server-agent-file-rotation"></a>

Each EnginFrame Server and EnginFrame Agent is configured to write log files up to 10 MB and then to create another file to a maximum of 4 files\. When a new log file is written the oldest one is deleted\. This configuration guarantees that each server and agent uses no more than 40 MB of disk space for log files\. You may want to change this rotation policy for example because you need more history\. A change may also be helpful if you have increased log verbosity\.

Changing the `<rotation>` tag inside the `<targets>` section configures the rotation policy\. The `max` attribute defines the maximum number of files, while the `<size>` tag contains each file's size\.

For example the following XML text defines a rotation of 5 files each one of 5 MB:

```
<rotation type="revolving" max="5">
  <size>5m</size>
</rotation>
```

### Change log level<a name="section-logging-server-agent-verboseness"></a>

EnginFrame logging allows to have a fine grain control over which statements are printed\. In a development environment, you might want to enable all logging statements while in a production environment it is suggested to disable debug messages to avoid performance issues\. You can configure this behavior by setting the appropriate *log level*\. A *log level* describes the urgency of a message\. Below is a list of log levels that are usable within the EnginFrame logging system:
+ `NONE`: No messages are emitted\.
+ `DEBUG`: Developer\-oriented messages, usually used during development of the product\.
+ `INFO`: Useful information messages such as state changes, client connection, and user login\.
+  `WARN`: A problem or conflict has occurred but it may be recoverable, then again it could be the start of the system failing\. 
+ `ERROR`: A problem has occurred but it is not fatal\. The system still functions\.
+  `FATAL_ERROR`: Something caused whole system to fail\. This indicates that an administrator should restart the system and try to fix the problem that caused the failure\. 

Each logger instance is associated with a log level\. This allows you to limit each logger so that it only displays messages greater than a certain level\. So if a DEBUG message occurred and the logger's log level was WARN, the message would be suppressed\. 

Changing the `log-level` attribute of a `<category>` tag sets log verbosity for the associated category\. 

For example, this XML tag defines a default category whose log\-level is INFO:

```
<category name="" log-level="INFO">
  <log-target id-ref="core"/>
</category>
```

### Fine tune logging<a name="section-logging-configuration-fine-tune"></a>

#### Define new categories and targets<a name="section-logging-configuration-fine-tune-categories"></a>

In a complex system, it's often not enough to suppress logging based on log\-level\. For instance, you might want to log the network subsystem with `DEBUG` log\-level while the simulator subsystem with `WARN` log\-level\. To accomplish this EnginFrame uses *categories*\. Each `category` is a name, made up of name components separated by a "**\.**"\. So a category named "network\.interceptor\.connected" is made up of three name components "network", "interceptor" and "connected", ordered from left to right\. Every logger is associated with a category at creation\. The left\-most name component is the most generic category while the right\-most name component is the most specific\. So "network\.interceptor\.connected" is a child category of "network\.interceptor", which is in turn a child category of "network"\. There is also a root category *""* that is hidden\. The main reason for structuring logging namespace in a hierarchical manner is to allow inheritance\. A logger will inherit its parent log\-level if it has not been explicitly set\. This allows you to set the "network" logger to have INFO log\-level and unless the "network\.interceptor" has had its log\-level set it will inherit the INFO log\-level\.

Categories send messages to log targets\. Decoupling log message generation from handling allows developers to change destinations of log messages dynamically or via configuration files\. Possible destinations include writing to a database, a file, an IRC channel, a syslog server, an instant messaging client, etc\.

Adding a `<category>` tag inside the `<categories>` section defines a new category\. You must specify its `name` and `log-target` to which log messages are written\. The name of the category acts like a filter: all messages matching the category name are sent to the specified log\-target\.

For example, if you want more information from EnginFrame's download component you can use the category named `com.enginframe.server.download`:

```
<category name="com.enginframe.server.download" log-level="DEBUG">
  <log-target id-ref="core"/>
</category>
```

This configuration sends all download messages to the core target\. 

Another useful category is the `deadspooler`\. The deadspooler category is used by EnginFrame to write messages concerning spoolers that could not be deleted and were renamed as DEAD\. NICE support team recommends to turn this feature on\. There is no overhead and it could be very useful to know why an EnginFrame spooler could not be deleted\. This category is activated by setting its log\-level to `INFO`: 

```
<category name="deadspooler" log-level="INFO">
  <log-target id-ref="deadspooler"/>
</category>
```

Refer to *EnginFrame Administrator Reference* for a complete list of categories EnginFrame uses\. 

#### Change message format<a name="section-logging-configuration-fine-tune-formatters"></a>

Log targets that write to a serial or unstructured store \(i\.e\., file\-system or network based targets\) need some method to serialize the log message before writing to the store\. The most common way to serialize the log message is to use a `formatter`\.

The format specified consists of a string containing raw text combined with pattern elements\. Each pattern element has the generalized form:

```
%[+|-]#.#{field:subformat}
```
+ `+|-` indicates whether the pattern element should be left or right justified \(defaults to left justified if unspecified\.\)
+ `#.#` indicates the minimum and maximum size of output, if unspecified the output is neither padded nor truncated\.
+ `field` indicates the field to be written and must be one of `category`, `context`, `user`, `message`, `time`, `rtime` \(time relative to start of application\), `throwable` or `priority`\. This parameter is mandatory\.
+ `subformat` specifies which piece of field is interesting for log messages\.

Use the `<format>` tag to set log message printing\.

For example the following code shows format setting for the `core` target:

```
<enginframe id="core">
  <filename>${EF_LOGDIR}/ef.log</filename>
  <format type="enginframe">
    %7.7{priority} %5.5{rtime} [%8.8{category}]:%{message}\n%{throwable}
  </format>
  ...
```

A number of examples for format and actual output follows\.
+ Example

  Format:

  ```
  %7.7{priority} %5.5{rtime} [%8.8{category}]:%{message}\n%{throwable}
  ```

  Output:

  ```
  DEBUG   123   [network.]: This is a debug message
  ```
+ Example

  Format:

  ```
  %7.7{priority} %5.5{rtime} [%{category}]:%{message}\n
  ```

  Output:

  ```
  DEBUG   123   [network.interceptor.connected]: This is a debug message
  DEBUG   123   [network]: This is another debug message
  ```
+ Example

  Format:

  ```
  %7.7{priority} %5.5{rtime} [%10.{category}]:%{message}\n
  ```

  Output:

  ```
  DEBUG   123   [network.interceptor.connected]: This is a debug message
  DEBUG   123   [network   ]: This is another debug message
  ```

## EnginFrame scriptlet logging<a name="section-logging-scriptlet-logging"></a>

EnginFrame modularity lets developers add new features by deploying their plugins\. If your plugin uses scriptlets, you have the same logging support on which EnginFrame is based\. As an administrator you must know how to set up scriptlet logging for both development and production environments\.

Creating `$EF_TOP/<VERSION>/enginframe/plugins/<myplugin>/conf/log.xconf` or `$EF_TOP/conf/plugins/<myplugin>/log.xconf` on EnginFrame Server's host enables scriptlet logging\. This file has the same syntax as the ones shipped by EnginFrame under `$EF_TOP/<VERSION>/enginframe/conf`, so all the information in [EnginFrame server and agent logging](#section-logging-server-agent) applies here too\.

The scriptlet code can emit logging messages with any category and log level\. 

This is an example configuration file:

```
<?xml version="1.0"?>

<logkit>
  <factories>
    <factory
        type="enginframe"
        class="com.enginframe.common.utils.log.EnginFrameTargetFactory"/>
  </factories>

  <targets>
    <enginframe id="plugin">
      <filename>
        ${EF_LOGDIR}/myplugin.log
      </filename>
      <format type="enginframe">
        %7.7{priority} %5.5{rtime} [%{category}]:%{message}\n
      </format>
    </enginframe>
  </targets>

  <categories>
    <category name="myplugin" log-level="DEBUG">
      <log-target id-ref="plugin"/>
    </category>
    <category name="" log-level="WARN">
      <log-target id-ref="plugin"/>
    </category>
  </categories>
</logkit>
```

`${EF_LOGDIR}/<myplugin>.log` contains the log messages for this configuration\. It exposes only two categories: `myplugin` and the `root one` \(it is the one that has an empty name\.\) If your code uses `myplugin` category, then it logs `DEBUG` messages; if your code uses a category that is not defined, then it logs `WARN` messages\.

If the plugin log\.xconf configuration files don't exist, then EnginFrame defaults to the core `log.server.xconf` to define myplugin's logging categories\.