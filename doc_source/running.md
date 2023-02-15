# Running NICE EnginFrame<a name="running"></a>

This chapter describes how to start and stop EnginFrame Portal and check its status\. It also covers administration monitoring and self\-check services\. 

## Start or stop EnginFrame and check its status<a name="start-stop-status"></a>

You can control EnginFrame with the $EF\_TOP/bin/enginframe command line script\. 

Run the following command to start EnginFrame: 

```
# $EF_TOP/bin/enginframe start
```

Run the following command to stop EnginFrame: 

```
# $EF_TOP/bin/enginframe stop
```

**Note**  
If EnginFrame Server and EnginFrame Agent are on separate hosts, run the following command on the host that's running EnginFrame Server:   

```
# $EF_TOP/bin/enginframe <start|stop> server
```
Run the following command on the host that's running EnginFrame Agent:  

```
# $EF_TOP/bin/enginframe <start|stop> agent
```

**Note**  
To start EnginFrame Enterprise, run the EnginFrame start \(stop\) command on each host of the EnginFrame Enterprise infrastructure that's in your deployment\. For more information, see [Deployment](about.md#enterprise-deployment)\.  

```
# $EF_TOP/bin/enginframe <start|stop>
```

This control script also checks EnginFrame's status: 

```
# $EF_TOP/bin/enginframe status
```

The output of the previous command is as follows:

```
# /opt/nice/enginframe/bin/enginframe start

Reading EnginFrame version from: /opt/nice/enginframe/current-version
Current version: 2017.0-r41442

EnginFrame Control Script
Loading configuration from:
 - "/opt/nice/enginframe/conf/enginframe.conf"
Using EnginFrame in "/opt/nice/enginframe/2017.0-r41442"
Tomcat started.

[OK] EnginFrame Server started

[OK] EnginFrame Agent started
```

```
# /opt/nice/enginframe/bin/enginframe status
Reading EnginFrame version from: /opt/nice/enginframe/current-version
Current version: 2017.0-r41442

EnginFrame Control Script
Loading configuration from:
 - "/opt/nice/enginframe/conf/enginframe.conf"
Using EnginFrame in "/opt/nice/enginframe/2017.0-r41442"

---- Server PID Information ----
USER       PID  PPID %CPU %MEM STIME     TIME COMMAND
efnobody  1674     1 69.9 17.4 19:34 00:01:47 /usr/lib/jvm/jre/bin/java
-Xms1024m -Xmx1024m -XX:HeapDumpPath=/[...]/dumps/server.pid1549.hprof
-Djava.protocol.handler.pkgs=com.enginframe.common.utils.xml.handlers
-XX:ErrorFile=/[...]/dumps/server.hs_err_pid1549.log
-DjvmRoute=efserver1 -DEF_LICENSE_PATH=/opt/nice/enginframe/license
-DDERBY_DATA=/opt/nice/enginframe/data/derby -DEF_ERRORS_DIR=/opt/nice/
enginframe/data/errors -Def.repository.dir=/opt/nice/enginframe/repository
-XX:+HeapDumpOnOutOfMemoryError -DEF_ROOT=/opt/nice/enginframe/2017.0-r41442/
enginframe -DEF_DYNAMIC_ROOT=/opt/nice/enginframe/2017.0-r41442/enginframe
-DEF_CONF_ROOT=/opt/nice/enginframe/conf -DEF_DATA_ROOT=/opt/nice/enginframe/
data -Def.tmp.dir=/opt/nice/enginframe/tmp/efserver1 -DEF_SPOOLER_DIR=/opt/
nice/enginframe/spoolers -DEF_SESSION_SPOOLER_DIR=/opt/nice/enginframe/
spoolers -DEF_LOGDIR=/opt/nice/enginframe/logs/efserver1
-Dfile.encoding=UTF -classpath :/opt/nice/enginframe/2017.0-r41442/tomcat/lib/
sdftree-handler.jar:/opt/nice/enginframe/2017.0-r41442/tomcat/bin/
bootstrap.jar:/opt/nice/enginframe/2017.0-r41442/tomcat/bin/tomcat-juli.jar
 [...] org.apache.catalina.startup.Bootstrap start

---- Server Port Information ----
INFO: Starting ProtocolHandler ["http-bio-8443"]

---- Agent PID Information ----
root      1677     1  6.5  5.2 19:34 00:00:10 /usr/lib/jvm/jre/bin/java
-Xms512m -Xmx512m -XX:HeapDumpPath=/[...]/dumps/agent.pid1549.hprof
-XX:ErrorFile=/[...]/dumps/agent.hs_err_pid1549.log
-DEF_ROOT=/opt/nice/enginframe/2017.0-r41442/enginframe -DEF_DYNAMIC_ROOT=
/opt/nice/enginframe/2017.0-r41442/enginframe -DEF_CONF_ROOT=/opt/nice/
enginframe/conf -DEF_DATA_ROOT=/opt/nice/enginframe/data -DEF_SPOOLER_DIR=
/opt/nice/enginframe/spoolers -DEF_SESSION_SPOOLER_DIR=/opt/nice/enginframe/
spoolers -DEF_LOGDIR=/opt/nice/enginframe/logs/efserver1 -Dfile.encoding=UTF-8
-Djava.security.policy==/[...]/2017.0-r41442/enginframe/conf/ef_java.policy
 [...] -jar /opt/nice/enginframe/2017.0-r41442/enginframe/agent/agent.jar
```

```
# /opt/nice/enginframe/bin/enginframe stop

Reading EnginFrame version from: /opt/nice/enginframe/current-version
Current version: 2017.0-r41442

EnginFrame Control Script
Loading configuration from:
 - "/opt/nice/enginframe/conf/enginframe.conf"
Using EnginFrame in "/opt/nice/enginframe/2017.0-r41442"
Tomcat stopped.

[OK] EnginFrame Agent is down
```

## Accessing the portal<a name="accessing-portal"></a>

After the EnginFrame daemons are running, you can access EnginFrame Portal in a browser window\. To do this, in the browser's address bar, enter the host name of your EnginFrame Server followed by a colon \(:\) and your EnginFrame Server port number\. 

The EnginFrame Server port number was set during installation and can be viewed with the the following command\.

```
# $EF_TOP/bin/enginframe status
```

For example, if the EnginFrame Server host is named *myhost*, and EnginFrame Server port number is `7070`, type in your browser's address bar as follows: 

`http://myhost:7070`

If your host name \(in this example, `myhost`\) isn't resolved by your DNS, you can specify the corresponding IP address:

`http://192.168.0.10:7070`

**Note**  
If you encounter an issue related to the DNS name, domain resolution, or the IP address, contact your network administrator for help\. 

If EnginFrame Server is installed successfully, the welcome page is displayed when you access the portal\. If your browser reports errors such as `Cannot find the requested page`, `Server not found`, or `Problem loading page`, verify that EnginFrame is installed correctly by checking its status as described in [Start or stop EnginFrame and check its status](#start-stop-status)\. 

## Demo sites<a name="demo-sites"></a>

If you installed the EnginFrame *Developer's Documentation* when you installed EnginFrame, the welcome page, together with the production portal `Applications`, `Views`, and `Operational Dashboard`, displays a link to the `Technology Showcase`, which points to a set of demo services\. These demo services provide an illustration of all of EnginFrame's service capabilities\.

**Important**  
By default, only the `EF_ADMIN` user can access administration and tutorial demo sites\. 

## Operational Dashboard<a name="admin-portal"></a>

In the EnginFrame *Operational Dashboard* view, administrators can monitor and manage operations directly from a web browser\. 

The Operational Dashboard is linked from the EnginFrame welcome page\. Otherwise, you can reach it directly at: 

`http://host:port/context/admin` 

The Operational Dashboard offers a set of services that are divided into the following categories: 

**Topics**
+ [Monitor](#monitor-services)
+ [Troubleshooting](#troubleshooting-services)
+ [EnginFrame statistics](#statistics)

These services are listed in the navigation pane of the dashboard\.

### Monitor<a name="monitor-services"></a>

You can view and use the services listed in **Monitor**\.
+ **Server Load** shows CPU usage, Java™ Virtual Machine memory usage, repository and spoolers file system size, and i\-node usage\. 
+ **Usage Statistics** shows current and historical data for the number of logged users, jobs with status, and interactive sessions and spoolers\. 
+ **Installed Components** displays the list of installed EnginFrame plugins and versions\. 
+ **Logged Users** shows the users logged into the portal, including an option to force user logout\. 
+ **Triggers** can be used view and manage scheduled triggers in EnginFrame\. 
+ **ACL Actors** shows EnginFrame ACL actors defined in the `authorization.xconf` files that are loaded by the system\. 

### Troubleshooting<a name="troubleshooting-services"></a>

With the services listed in **Troubleshooting**, you can check portal status and health\.
+ **Run Self checks** performs several operations to exercise different functions and aspects of EnginFrame\. Every test outputs a result and, in most cases, a quick hint to correct the problem\. 
+ **View Error Files** can be used to display error files generated by EnginFrame when services produce the wrong output\. You can choose an error to view by entering the error file name, by selecting errors from a list, or by entering an error number\. 
+ **Collect Support Info** gathers a wide range of information about EnginFrame Portal and its configuration\. This service output is a compressed archive containing all gathered information\. Attach this package when sending your request to EnginFrame support\. 

### EnginFrame statistics<a name="statistics"></a>

To collect information about license usage, jobs usage, and others useful statistics, EnginFrame uses RRD4J as round\-robin database\. 

RRD4J is a high\-performance data logging and graphing system for time series data, implementing [RRDTool's](http://oss.oetiker.ch/rrdtool/) functionality in Java™\. It follows much of the same logic and uses the same data sources, archive types, and definitions that RRDTool uses\. 

EnginFrame creates a database for general usage information that's named `efstatistics.rrd` and a database for each license file that's named `license_<component>_<expiration>_<maxToken>.rrd`\. A new database will be created when a license file changes\. 

In the `admin.statistics.efconf` configuration file, you can configure some RRD4J specific parameters to change archive time intervals or to configure historical charts\. For more information, see the [RRD4J](https://github.com/rrd4j/rrd4j) website\. 

When you run EnginFrame for the first time, database files are created and loaded with data, and then they're updated every 60 seconds with new data\. 

## Workspace<a name="applications-portal"></a>

In the EnginFrame *Workspace* view, users can create, manage, and submit both batch and interactive services\. 

The Workspace is linked from the EnginFrame welcome page or can be reached directly using the following URL\.

`http://<host>:<port>/<context>/applications` 

The Workspace offers two interfaces for two different user roles: *Admin View* and *User View*\. 

### Admin View<a name="admins-portal"></a>

You can use the *Admin View* interface to monitor interactive sessions, jobs, hosts, and to manage services, Workpsace users and portal appearance\.
+ *Monitor » All Sessions* can by used by the administrator to manage interactive sessions for all Workpsace users\. 
+ *Monitor » All Jobs* can be used by the administrator to monitor and manage DRM jobs for all Workpsace users\. To control the jobs of other users' Workpsace administrator must have the proper rights in the underlying DRM\. 
+ *Monitor » Hosts* can be used by the administrator to monitor the status of the hosts of the configured DRMs\. 
+ *Manage » Services* can be used by the administrator to create, delete, edit, or publish batch and interactive services\. 
+ *Manage » Users* service allows the administrator to register, import, or manage Workpsace users\. 
+ *Manage » Appearance* service enables the administrator to change the company logo and the Portal color theme\. 

### User View<a name="user-portal"></a>

You can use *User View* to monitor user data, sessions, jobs and hosts, together with Batch and Interactive services that are published by the Workspace administrators\. 
+ *Data » Spoolers* shows the user's EnginFrame Spoolers and provides rename and delete operations\. 
+ *Data » Files* allows the user to browse and manage files in their home directory\. 
+ *Monitor » Sessions* can be used by the user to monitor and manage their interactive sessions\. 
+ *Monitor » Jobs* can be used by the user to monitor and manage their jobs\. 
+ *Monitor » Hosts* can be used by the user to monitor the status of the hosts of the configured DRMs\. 

Workspace administrators can create and publish new services through the Admin View\. When they publish a new service, administrators can make it available to all users or only to specific groups of users\. 

**Note**  
The Workspace requires a specific license\. Contact helpdesk@nice\-software\.com or your EnginFrame reseller to purchase a license, perform a license change or obtain a demo license\. EnginFrame doesn't require a license on an EC2 instance\. For more information about licensing, see [Obtaining NICE EnginFrame](obtaining.md)\. 

## Virtual Desktop<a name="virtual-desktop"></a>

EnginFrame includes the *Virtual Desktop* to create, manage, and submit Interactive services\. 

The Virtual Desktop is linked from the EnginFrame welcome page or can be reached directly at

: `http://<host>:<port>/<context>/vdi` 

The Virtual Desktop offers two interfaces for two different users' roles: *Admin's Portal* and *User View*\. 

### Admin View<a name="admin-portal-views"></a>

You can use the *Admin View* to monitor and manage interactive sessions, jobs, hosts, services, users and portal appearance\.
+ *Monitor » All Sessions* can be used by the administrator to manage interactive sessions for all Virtual Desktop users\. 
+ *Monitor » Hosts* can be used by the administrator to monitor the status of the hosts of the configured DRMs\. 
+ *Manage » Interactive Services* can be used by the administrator to create, delete, edit, or publish Interactive services\. 
+ *Manage » Users* can be used by the administrator to register, import, and manage Virtual Desktop users\. 
+ *Manage » Appearance* can be used by the administrator to change the company logo and the Portal color theme\. 

### User View<a name="user-portal-views"></a>

You can use the *User View* to monitor user's sessions and cluster hosts, together with the Interactive services published by Virtual Desktop administrators\.
+ *Monitor » Sessions* can be used by the user to monitor and manage their interactive sessions\. 
+ *Monitor » Hosts* can be used by the user to monitor the status of the hosts of the configured DRMs\. 

Virtual Desktop administrators can create and publish new services through the Admin View\. They can publish these services to specific users or groups of users\. 