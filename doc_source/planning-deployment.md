# Planning a NICE EnginFrame deployment<a name="planning-deployment"></a>

Setting up EnginFrame is a straightforward process\. However, it's important to accurately plan your EnginFrame Portal deployment to achieve seamless integration with your computing environment and to meet the IT requirements of your organization\.

**Note**  
Starting March 31, 2022, NICE EnginFrame doesn't support VNC®, HP® RGS, VirtualGL, and NICE DCV 2016 and previous versions\.

## Prerequisites<a name="checking-prerequisites"></a>

Before you deploy EnginFrame Portal, make sure that your system meets the following requirements\. 

**Topics**
+ [System requirements](#system-requirements)
+ [Third\-party software prerequisites](#third-party-prerequisites)
+ [Network requirements](#network-requirements)
+ [Supported browsers](#supported-browsers)
+ [Interactive Plugin requirements](#interactive-requirements)
+ [EnginFrame Enterprise system requirements](#ef-ent-system-requirements)

### System requirements<a name="system-requirements"></a>

**Topics**
+ [Additional considerations for using SUSE Linux](#sles-system-requirements)

NICE EnginFrame supports the following operating systems:
+ Amazon™ Linux® release 2016\.03 or later
+ Red Hat® Enterprise Linux® 5\.x, 6\.x, 7\.x, 8\.x \(*x86\-64*\)
+ SUSE® Linux® Enterprise Server 11 SP2, 12 SP3 \(*x86\-64*\)

  SUSE® Linux® Enterprise Server 12 SP5 \(*x86\-64*\)

  SUSE® Linux® Enterprise Server 15 SP2 \(*x86\-64*\)

**Note**  <a name="footnote-os-java-version"></a>
Other Linux® distributions and compatible Java™ versions might work but are not officially supported\. Contact helpdesk@nice\-software\.com for more information\. 

The installation machine must have at least 3 GB of RAM and one or more IP addresses\. For these IP addresses, at least one of them must be reachable by each of the potential client machines\. It can be reached either directly or through proxies\. 

To install EnginFrame, minimally you need at least 200 MB of free disk space\. However, we recommend that you have as much as 2 GB or more\. This is because EnginFrame while operating saves important data and logging information\. 

Make sure you have enough space for the service data that's stored inside the EnginFrame spoolers\. By default, spoolers are located inside the EnginFrame installation directory \(`$EF_TOP/spoolers`\)\. 

#### Additional considerations for using SUSE Linux<a name="sles-system-requirements"></a>

EnginFrame PAM standard user authentication \(system\) expects to find the file `system-auth` in the folder `/etc/pam.d/`\. However, in SUSE® Linux® Enterprise Server, this file is called `common-auth`\. So, to make the standard authentication work, a symbolic link is required: ` ln -s /etc/pam.d/common-auth /etc/pam.d/system-auth ` 

### Third\-party software prerequisites<a name="third-party-prerequisites"></a>

In addition to the standard packages that are installed with your operating system, NICE EnginFrame also requires some additional third\-party software\. This topic describes the third\-party software that's required and how you can set it up\.

**Topics**
+ [Java™ platform](#java-platform)
+ [Database management systems](#database)
+ [Authentication methods](#authentication-methods)
+ [Distributed resource managers](#distributed-resource-managers)
+ [Remote visualization technologies](#remote-visualization-technologies)

#### Java™ platform<a name="java-platform"></a>

NICE EnginFrame requires the *Linux® x64* version of *Oracle® Java™ Platform Standard Edition* \(Java™ SE\) or the *OpenJDK Runtime Environment *\. EnginFrame supports both versions 8 and 11 of these packages\.

**Supported Java™ vendors:**
+ Oracle®
+ Amazon Web Services
+ Red Hat®
+ IcedTea

In this topic, `JAVA_HOME` is referred to as the Java™ installation directory\.

The same Java™ version must be used for both EnginFrame Server and EnginFrame Agent\.

#### Database management systems<a name="database"></a>

EnginFrame requires a *JDBC\-compliant* database\. EnginFrame uses a relational database management system to manage *Triggers*, *Job\-Cache*, and *Applications* and *Views* user groups\. EnginFrame *Triggers* rely on Quartz \([http://www\.quartz\-scheduler\.org](http://www.quartz-scheduler.org/)\) engine to schedule EnginFrame services to run\. Triggers are used internally to run periodic tasks as to check and update Interactive sessions status\. They're also used to collect EnginFrame usage statistics\. The *Job\-Cache* feature is responsible for collecting and caching job statuses over time\.

By default, Apache Derby® 10\.14 database is installed together with EnginFrame Professional\. However, we don't recommend using Apache Derby® in a production installation\.

Apache Derby® isn't supported for EnginFrame Enterprise installations\. We recommend that you use an external JDBC\-compliant relational database management system \(RDBMS\)\. Because EnginFrame Enterprise is part of a high availability solution, the RDBMS that you choose to use must have its own high availability strategy\. We recommend that you configure the external RDBMS on a different node or nodes than the EnginFrame servers\. If possible, we also recommend that you configure it to be fault tolerant\.

EnginFrame supports MySQL® Database 8\.0\.x and later with the InnoDB storage engine\. You can also use EnginFrame with other databases, such as Oracle® Database, SQL Server®, MariaDB®\. However, these databases aren't officially supported, so we don't recommend that you use them\. If you encounter issues with a supported relational database management system version, contact helpdesk@nice\-software\.com\. 

EnginFrame provides the JDBC driver only for Apache Derby®\. If a different DBMS is used, you must add the JDBC driver to the `$EF_TOP/<VERSION>/enginframe/WEBAPP/WEB-INF/lib` directory after you install EnginFrame\.

For instructions on how to install and configure the JDBC driver, see [Install and configure EnginFrame](section-installation.md#config)\.

#### Authentication methods<a name="authentication-methods"></a>

You can use a variety of authentication methods with EnginFrame\. Some of them require third\-party software components\. 

We recommend that you consider a variety of factors when choosing an authentication method\. The following table details several relevant considerations including third\-party software prerequisites, if any exist\. For more information, see also [Supported authentication methods](#table-authentication-mechanisms)\. 

##### Supported authentication methods<a name="table-authentication-mechanisms"></a>

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/enginframe/latest/ag/planning-deployment.html)

The EnginFrame installer can optionally verify if you configured the selected authentication method\.

 NICE EnginFrame can be easily extended to add support for custom authentication mechanisms\. 

#### Distributed resource managers<a name="distributed-resource-managers"></a>

EnginFrame supports different distributed resource managers \(DRM\)\. 

When you install EnginFrame, you must specify which distributed resource managers that you want to use and provide the information that's required by EnginFrame to contact them\. A single EnginFrame instance can access more than one DRM at the same time\. 

##### Supported distributed resource managers<a name="table-supported-distributed-resource-managers"></a>

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/enginframe/latest/ag/planning-deployment.html)

By default, some schedulers such as PBS Professional® and Univa® Grid Engine® \(UGE\) 8\.2\.0 have job history disabled\. This means that a job disappears when finished\. We recommend that you configure these distributed resource managers to retain information about the finished jobs\. For more information, see [Required DRM configuration](#distributed-resource-managers-configuration)\.

**Note**  
Starting March 31, 2022, NICE EnginFrame doesn't support VNC®, HP® RGS, VirtualGL, and NICE DCV 2016 and previous versions\.

##### Required DRM configuration<a name="distributed-resource-managers-configuration"></a>

AWS HPC Connector  
For information, see [Requirements for running HPC Connector](https://docs.aws.amazon.com/enginframe/latest/ag/about.html#hpc-connector)\. 

Altair® PBS Professional®  
*Applies to versions: 11, 12, 14*  
 By default, Altair® PBS Professional® doesn't show finished jobs\. To enable job history, a server parameter must be changed: `qmgr -c "set server job_history_enable = True"`   
After it's enabled, the default duration of the job history is 2 weeks\.

Univa® Grid Engine® \(UGE\)  
*Applies to versions: 8\.2\.x*\.  
Univa® Grid Engine® \(UGE\) by default does not show finished jobs\. To enable job history, follow these steps:  
+ *\(8\.2\.0 only\)* disable reader threads:

  Edit file `SGE_ROOT/SGE_CELL/common/bootstrap`\.

  Set `reader_threads` to 0 instead of 2\.
+ Enable finished jobs:

  Run the `qconf -mconf` command\.

  Set `finished_jobs` to a non\-zero value according to the rate of finishing jobs\.

  The `finished_jobs` parameter defines the number of finished jobs stored\. If this maximum number is reached, the oldest finished job is discarded for every new job that's added to the finished job list\.

  By default, EnginFrame grabs the scheduler jobs every minute\. The `finished_jobs` parameter must be tweaked so that a finished job stays in the job list for at least a minute\. Depending on the number of jobs that are running in the cluster a reasonable value is in between *the medium number of running jobs* and *the amount of jobs ending per minute*\.
+ Run the `restart qmaster` command\.

SLURM™  
*Applies to versions: all*\.  
SLURM™ shows finished jobs for a default period that's defined by the `MinJobAge` parameter in the `slurm.conf` file\. It's under `/etc/slurm` or the SLURM™ configuration directory\. The default value is *300* seconds \(five minutes\)\.  
If you changed this parameter, ensure it's not set to a value lower than 300\.  
Check the `MaxJobCount` parameter isn't set\.  
After changing this parameter restart SLURM™ by running the `/etc/init.d/slurm stop /etc/init.d/slurm start` command\.  
You must set this setting on all SLURM™ nodes\.

IBM® Platform™ LSF®;  
*Applies to versions: all*\.  
IBM® Platform™ LSF® shows finished jobs for a default period that's defined by the `CLEAN_PERIOD` parameter in the `lsb.params` file\. The default value is 3600 seconds \(one hour\)\.  
If you changed this parameter, ensure it's not set to a value lower than 300\.  
After changing this parameter, run the `badmin reconfig` command\.

AWS Batch  
To integrate EnginFrame with AWS Batch, create an AWS Batch cluster with AWS ParallelCluster and give the user that's to run the EnginFrame server permission to interact with the cluster\. To do this, follow these steps\.  
+ Install AWS ParallelCluster and configure it\. For more information, see [Setting up AWS ParallelCluster](https://docs.aws.amazon.com/parallelcluster/latest/ug/install-v3.html) in the *AWS ParallelCluster User Guide*\.

  As a part of the setup process, [AWS CLI](http://aws.amazon.com/cli) is installed as dependency of AWS ParallelCluster\.
+ Install AWS ParallelCluster AWS Batch CLI 1\.0\.0\. It's distributed on PyPi as `aws-parallelcluster-awsbatch-cli`\.
+ Create a new cluster for the AWS Batch scheduler\. Make sure that, when you create the cluster, you take into account the network requirements for [AWS ParallelCluster with AWS Batch scheduler](https://docs.aws.amazon.com/parallelcluster/latest/ug/network-configuration-v3.html#network-configuration-v3-batch)\.
+ In the IAM console create a user *MY\_USER* with the following policy:

  ```
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": "sts:AssumeRole",
        "Resource": "<MY_ROLE_ARN>"
      }
    ]
  }
  ```

  For this policy, replace *<MY\_ROLE\_ARN>* with the ARN of the role that you create in the next step\. Keep note of the User credentials because you're going to use them later\.
+ In the IAM console, create a role *MY\_ROLE* that uses the policies "Base user policy" and "Additional user policy" when using AWS Batch scheduler"\. For more information, see [AWS Identity and Access Management roles in AWS ParallelCluster](https://docs.aws.amazon.com/parallelcluster/latest/ug/iam-roles-in-parallelcluster-v3.html) in the *AWS ParallelCluster User Guide*\. In addition, also include the following trust relationship\.

  ```
  {
    "Version":"2012-10-17",
    "Statement":[
      {
        "Effect":"Allow",
         "Action": "sts:AssumeRole",
         "Principal": {
           "AWS": "<MY_USER_ARN>"
         }
      }
    ]
  }
  ```

  Replace *MY\_USER\_ARN* with the ARN of the user that you created on the preceding step\.
+ Create a dedicated AWS profile with name *MY\_PROFILE* to use with the AWS CLI for the user running the EnginFrame Server \(for example, *efnobody*\) and configure it to use the credentials of *MY\_USER*\.

  ```
  [efnobody]$ aws configure --profile MY_PROFILE
  ```
+ Follow EnginFrame installer steps to configure AWS Batch EnginFrame plugin to contact the created cluster\.
+ When upgrading to EnginFrame 2021\.x, add the following lines in `$EF_CONF_ROOT/plugins/awsbatch/ef.awsbatch.conf` config file after it's upgraded the release with the installer:

  ```
   # AWS profile that the AWS Batch plugin should use to interact with AWS
   AWSBATCH_PROFILE=<MY_PROFILE>
    
   # AWS IAM role ARN that the AWS Batch plugin should use to interact with AWS Batch
   AWSBATCH_ROLE_ARN=<MY_ROLE_ARN>
  ```

  Replace *MY\_PROFILE* and *MY\_ROLE\_ARN* with the specific ones that you created in the preceding steps\.

#### Remote visualization technologies<a name="remote-visualization-technologies"></a>

EnginFrame supports different remote visualization technologies, and the same EnginFrame instance can manage more than one of these visualization technologies\. The following table lists the supported ones\.


**Supported remote visualization technologies**  

|  Name  |  Version  |  Notes  | 
| --- | --- | --- | 
|  NICE DCV  |  2017\.x or later  |  You can use it to share sessions both in full access or view only mode\.  | 
|  NICE DCV Session Manager  |    |  For more information, see the [NICE DCV Session Manager documentation](https://docs.aws.amazon.com/dcv/#nice-dcv-session-manager)  | 

For instructions on how to install and configure these remote visualization technologies, see their respective manuals\. 

**Note**  
Starting March 2022, EnginFrame doesn't support TurboVNC, in favor of NICE DCV Session Manager\. Customers using versions of EnginFrame released after March 2022 will be unable to use TurboVNC for accessing interactive sessions\.

##### Remote visualization technologies configuration<a name="remote-visualization-technologies-configuration"></a>

##### NICE DCV 2017\.0 or later on Linux<a name="remote-visualization-technologies-configuration-on-linux"></a>

For Linux environments, the authentication configuration to use with NICE DCV must correspond to the authentication system that's set on the NICE DCV server in the remote visualization hosts\.

On EnginFrame, the authentication to use with NICE DCV on Linux can be set in the `INTERACTIVE_DEFAULT_DCV2_LINUX_AUTH` configuration parameter that's in the `$EF_TOP/conf/plugins/interactive/interactive.efconf` file\.

The default value and documentation can be found in the static configuration file that's named `$EF_TOP/<VERSION>/enginframe/plugins/interactive/conf/interactive.efconf`\.

The `auto` authentication system provides seamless authentication with self\-generated strong passwords\. It requires the following configuration on the visualization hosts that are running the NICE DCV server\.
+ Make sure that the NICE DCV simple external authenticator that's provided with NICE DCV is installed and running\.

   The simple external authenticator installation package is distributed as an rpm \(for example, `nice-dcv-simple-external-authenticator-2017.x...x86_64.rpm`\)\. 

  After it's installed, you can manage the service as `root` user:
  + On systems using `SystemD` \(for example, RedHat 7\):

    ```
    $ systemctl [start|stop|status] dcvsimpleextauth
    ```
  + On systems using `SysVInit` \(for example, RedHat 6\):

    ```
    $ /etc/init.d/dcvsimpleextauth [start|stop|status]
    ```
+ You must configure the NICE DCV server to use the simple external authenticator instance that's named `dcvsimpleextauth` to run on the same host\. For example, configure it to run by editing the `/etc/dcv/dcv.conf` file, under the `security` section as follows:

  ```
  [security]
  auth-token-verifier="http://localhost:8444"
  ```
+ Restart the NICE DCV server after changes were made to the `/etc/dcv/dcv.conf` configuration file\.

##### NICE DCV 2017\.0 or later on Windows<a name="remote-visualization-technologies-configuration-on-windows"></a>

For Windows environments the authentication configuration used with NICE DCV must be configured on EnginFrame in the `INTERACTIVE_DEFAULT_DCV2_WINDOWS_AUTH` configuration parameter\. This is in the `$EF_TOP/conf/plugins/interactive/interactive.efconf` file\.

Default value and documentation can be found in the `$EF_TOP/<VERSION>/enginframe/plugins/interactive/conf/interactive.efconf` static configuration file\. 

The `auto` authentication system provides seamless authentication with self\-generated strong passwords\. It doesn't require any other configuration on the visualization hosts that are running the DCV server\. 

 The DCV server service is managed by the interactive session job landing on the node:
+ If the NICE DCV server service is not running, it's started\.
+ If the NICE DCV server service is running but with different authentication configuration than the one set on the EnginFrame side, the configuration is changed and the service restarted\. This is also the case if the DCV server is configured to launch the console session at system startup\. This setting is removed by the interactive session job\.
+ If the NICE DCV session is running but there's no logged user, the session is closed by the interactive session job\.

### Network requirements<a name="network-requirements"></a>

EnginFrame is a distributed system\. Your network and firewall configuration must allow EnginFrame components to communicate with each other and with user browsers\. 

The specific requirements depend on how EnginFrame is deployed on your system\. The following table summarizes network requirements for a basic EnginFrame deployment\. 


**Network requirements**  

| Port \(default\) | Protocol | From host | To host | Mandatory | 
| --- | --- | --- | --- | --- | 
| 8080/8443 | HTTP/HTTPS | User's clients | EnginFrame Server | Mandatory | 
| 9999 and 9998 | RMI \(TCP\) | EnginFrame Server | EnginFrame Agent | Optional   | 
| 8080/8443 | HTTP/HTTPS | EnginFrame Agent | EnginFrame Server | Optional † | 
| 7800 | TCP | EnginFrame Server | EnginFrame Server | Mandatory only for EnginFrame Enterprise ‡  | 

† Required if EnginFrame Agent and EnginFrame Server run on separate hosts

‡ EnginFrame Servers use the port to communicate with each other

### Supported browsers<a name="supported-browsers"></a>

NICE EnginFrame produces HTML that can be viewed with most popular browsers\. NICE EnginFrame was tested with the browsers that are listed in [Supported browsers](#table-supported-browsers)\. 

#### Supported browsers<a name="table-supported-browsers"></a>


|  Name  |  Version  |  Notes  | 
| --- | --- | --- | 
|  Microsoft® Edge  |  41 and 44  | 
|  Microsoft® Internet Explorer®  |  10 and 11 \(Will be discontinued\)  | 
|  Mozilla Firefox®  |  3\.6 and later  | 
|  Apple® Safari®  |  6\.0 and later and iOS 6 version  |  Tested on Mac® OS X® and iPad® only\.  | 
|  Google™ Chrome™  |  25 and later  | 

JavaScript® and Cookies must be enabled on browsers\. 

By the end of December 2021, we will discontinue support for Internet Explorer 10\. Then, at the end of June 2022, we will discontinue support for Internet Explorer 11\. 

### Interactive Plugin requirements<a name="interactive-requirements"></a>

 Interactive Plugin requires the following components to be successfully installed and configured:
+ At least one supported resource manager software or a session manager\. For more information, see [Distributed resource managers](#distributed-resource-managers) and [Session Managers](#session-manager)\.
+ At least one supported remote visualization middleware\. For more information, see [Remote visualization technologies](#remote-visualization-technologies)\.

When running EnginFrame on an Amazon EC2 instance, you can use the Interactive Plugin without a license\. When running on an on\-premises or alternative cloud\-based server, you need a license that's installed on the EnginFrame Server\. 

Make sure that each node that's running interactive sessions has all the necessary software installed\. On Linux®, this usually means the packages for the desired desktop environment, such as gnome, kde, or xfce\. 

In addition, install the following software make it available in the system PATH on visualization nodes\. When you do this, the portal can show screen thumbnails in the session list\.
+ Linux®: *ImageMagick tool* \([http://www.imagemagick.org](http://www.imagemagick.org)\) and the `xorg-x11-apps, xorg-x11-utils` packages
+ Windows®: *NICE Shot tool* \(`niceshot.exe`, available under `$EF_TOP/<VERSION>/enginframe/plugins/interactive/tools/niceshot`\)\.

#### Session Managers<a name="session-manager"></a>

Starting from version 2020\.0, EnginFrame supports NICE DCV Session Manager as Session Broker\. 

When you install EnginFrame, you can choose to use NICE DCV Session Manager as session broker\. Then, provide the configuration parameters that are required by EnginFrame to contact the remote NICE DCV Session Manager Server\. 

#### Single application desktop requirements \(Linux®\)<a name="interactive-requirements-minimal"></a>

In some workflows, you might want to run a minimal session on your interactive nodes consisting in a minimal desktop and a single application running\. For this use case, instead of installing a full desktop environment such as GNOME or KDE, we recommend that you only install the required tools\. The required tools are a Window manager, a dock panel, and any of the applications that you intend to use\. 

In this example scenario, you can configure the `minimal.xstartup` script to be a Window Manager choice for the Applications and Views service editors\.

Here is a reference list of the tools that the `minimal.xstartup` file uses\. The file is provided by EnginFrame under `$EF_TOP/<VERSION>/enginframe/plugins/interactive/conf`\.
+ **basic tools:** `bash`, `grep`, `cat`, `printf`, `gawk`, `xprop`
+ **window managers:** `metacity`, `kwin` \(usually provided by package `kdebase`\), `xfwm4`
+ **dock panels:** `tint2`, `fluxbox`, `blackbox`, `mwm` \(usually provided by package `openmotif` or `lesstif` or `motif`\)

#### Shared file system requirements<a name="interactive-shared-file-system-requirements"></a>

Depending on the deployment strategy, EnginFrame might require some directories to be shared between the cluster and EnginFrame nodes\. This guide covers a scenario where both EnginFrame Server and EnginFrame Agent run on the same host\. For more complex configurations or to change the mount points of the shared directories, see the *"Deployment Strategies"* section in the EnginFrame Administrator Guide\. 

In this scenario the EnginFrame Server, EnginFrame Agent and visualization nodes might require the `$EF_TOP/sessions` directory to be shared\. To check if you need to share this directory, see the following table\. 


**Shared File System Requirement**  

|  Distributed Resource Manager  |  Linux®  |  Windows®  | 
| --- | --- | --- | 
| IBM® Platform™ LSF® | Not required | \- | 
| SLURM™ | Required | \- | 
| Altair® PBS Professional® | Required | \- | 
| Grid Engine \(SGE, SoGE, OGE, UGE\) | Required | \- | 

### EnginFrame Enterprise system requirements<a name="ef-ent-system-requirements"></a>

 This topic lists the hardware and software prerequisites for an EnginFrame Enterprise installation\. 

#### Shared file system<a name="shared-file-system"></a>

The suggested and supported approach to EnginFrame Enterprise deployment involves a shared file\-system for the whole $EF\_TOP directory tree\. Using this approach, you can install and manage the software from just one node, and all the binaries and data directories, such as the spoolers, sessions, and license, are shared among the installation nodes\. High\-Availability of the Shared File System is consistent with the overall HA/Disaster Recovery strategy\. 

The NFS `no_root_squash` or equivalent feature must be active to allow the correct management of permissions and ownership of deployed files\. 

We recommend that you enable on the shared file system the NFS `no_wdelay` or equivalent feature \(server\-side\) to minimize the file writing delay between clients\. 

#### Network load balancing<a name="network-load-balancing"></a>

To ensure automated load balancing and high availability for the EnginFrame services, it's necessary to set up a network load balancer that dispatches users' requests to the EnginFrame Servers in a balanced way\. 

EnginFrame requires the load balancer to implement a *sticky session* strategy\. There are many open\-source and commercial solutions to implement a network load balancer\. 

For examples of Apache® frontend configurations, see [Installing a third\-party Load Balancer](section-installation.md#ef-ent-installation-load-balancer)\. 

## Deployment strategies<a name="deployment-strategies"></a>

Decide how to deploy NICE EnginFrame on your system\.

As described in [Architectural overview](about.md#architecture), EnginFrame consists of two main software components: the EnginFrame Server and the EnginFrame Agent\. 

You can deploy these two components on the same host or on different hosts that communicate across the network\. We recommend that you deploy them based on the specifics of your computational resources organization, your network architecture, and your security and performance requirements\. In addition, before you deploy them, make sure that the following requirements are met\.
+ EnginFrame Server host must be reachable by HTTP or HTTPS by the clients and the EnginFrame Agents\. 
+ EnginFrame Agent host must have access to your computational resources and your grid infrastructure \(for example, to submit jobs to your scheduler\)\. 
+ EnginFrame Server and EnginFrame Agent must be installed on a shared storage area\. 
+ For the interactive sessions, EnginFrame Server and EnginFrame Agent must have read and write access to a storage area shared among them and with the visualization nodes\. 

If both EnginFrame Server and EnginFrame Agent run on the same host, communication between the two is reliable and minimizes administration efforts\. We recommend you use this deployment strategy if you have multiple EnginFrame installations on different hosts and on each of the hosts you install both an EnginFrame Server and Agent\. We recommend this deployment strategy for enterprise\-level deployments\. For more information, see [Deployment](about.md#enterprise-deployment)\. Make sure that the EnginFrame Servers can communicate with each other\.

Depending on your specific use case, you might want to install EnginFrame Server and EnginFrame Agent on separate hosts\. For example, you can run the EnginFrame Server in DMZ and EnginFrame Agent on the head node of your cluster\. For this deployment scenario, make sure that the following conditions are met\.
+ The Agent and Server must be able to communicate through a TCP connection using the [Java™ RMI protocol](http://docs.oracle.com/javase/8/docs/technotes/guides/rmi/index.html)\. The relevant TCP ports that are `9999` for RMI Registry and `9998` for Remote Object, must be free on the Agent's host and reachable from the Server host\. 
+ The Agent and Server must be able to communicate through a TCP connection using the HTTP or the HTTPS protocol\. By default, the relevant TCP port is `8080/8443` for HTTP/HTTPS, respectively, on the Server's host must be reachable from the Agent host\.
+ The Agent and Server must be installed on a shared storage area\.
  + The spoolers directory must reside on a storage area to meet the requirements that are described in the "Spoolers Requirements" section of the *EnginFrame Administrator Guide*\.
  + The sessions directory must reside on a storage area to meet the requirements that are described in EnginFrame [System requirements](#system-requirements)\.

If you need to access the system through a DMZ, you can use an Apache® web server as frontend in the DMZ when EnginFrame is deployed on the intranet\. With EnginFrame Enterprise, you can additionally use an Apache® server as network load balancer in front of a battery of EnginFrame Servers\. Make sure that the EnginFrame Server is behind the Apache® Web Server that forwards all the EnginFrame requests to the Tomcat® servlet container of the EnginFrame deployment\. For more information, see [Apache®\-Tomcat® connection](common-admin-tasks.md#apache-tomcat)\. 

By default, EnginFrame uses Java RMI over SSL between the Server and Agent\. You can set up Tomcat® when you install EnginFrame to use HTTPS\. Alternatively, you can also enable HTTPS after you install EnginFrame\. For instructions, see [Configuring HTTPS](http-ssl.md)\.  

## Installation directories<a name="installation-paths"></a>

The *installation directory* is the location, hereafter referred to as `$NICE_ROOT`, where EnginFrame binaries, configuration files, and logs are placed\. 

When you install EnginFrame, the following directory structure is created under `$NICE_ROOT`\.

```
  NICE_ROOT
  `-- enginframe
      |-- 2021.1-rXXXXX
      |   `-- enginframe
      |-- current-version
      |-- bin
      |   `-- enginframe
      |-- install
      |   `-- 2021.1-rXXXXX
      |-- license
      |   `-- license.ef
      |-- conf
      |   |-- enginframe.conf
      |   |-- enginframe
      |   |   |-- certs
      |   |   |-- server.conf
      |   |   `-- agent.conf
      |   |-- tomcat
      |   |   `-- conf
      |   |      `-- certs
      |   |-- derby
      |   |   |-- derby.properties
      |   |   `-- server.policy
      |   `-- plugins
      |-- data
      |   |-- cache
      |   |-- derby
      |   |   `-- EnginFrameDB
      |   `-- plugins
      |-- logs
      |   `-- <HOSTNAME>
      |       |-- *.log
      |       |-- tomcat
      |       `-- derby
      |-- repository
      |-- sessions
      |-- spoolers
      `-- temp
          `-- <HOSTNAME>
              |-- dumps
              |-- errors
              `-- tomcat
```

The following names are used in this guide to refer to the different parts of the EnginFrame installation tree\.

NICE\_ROOT  
The directory that contains all the NICE products\. By default, this directory is named `/opt/nice`\.

EF\_TOP  
The directory that contains the EnginFrame product\. By default, this directory is named `NICE_ROOT/enginframe`\.

EF\_LICENSE\_PATH  
The directory that contains the EnginFrame license files\. By default, it's named `EF_TOP/license`\.

EF\_CONF\_ROOT  
The directory that contains the EnginFrame configuration files\. By default, it's named `EF_TOP/conf`\.

EF\_DATA\_ROOT  
The directory that contains the data files\. By default, it's named `EF_TOP/data`\.

EF\_LOGS\_ROOT  
The directory that contains the log files\. By default, it's named `EF_TOP/logs`\.

EF\_TEMP\_ROOT  
The directory that contains the temporary files\. By default, it's named `EF_TOP/tmp`\.  
If you're using or planning to use the AWS HPC Connector plugin, make sure that `EF_TEMP_ROOT` points to a folder on a file system that's shared among the EnginFrame nodes\.

EF\_REPOSITORYDIR  
The directory that contains the EnginFrame repository files\. By default, it's named `EF_TOP/repository`\.

EF\_SPOOLERDIR  
The directory that contains the EnginFrame spoolers\. By default, it's named `EF_TOP/spoolers`\.

INTERACTIVE\_SHARED\_ROOT  
The directory that contains the EnginFrame interactive sessions\. By default, it's named `EF_TOP/sessions`\.

EF\_ROOT  
The directory that contains the EnginFrame binaries and system files\. By default, it's named `EF_TOP/<VERSION>/enginframe`\.

****  
The `PAM` based authentication method that's included with EnginFrame requires that some binaries have the `suid` bit set to interact with the underlying system to authenticate users\.   
If you plan to use this authentication method, make sure that the file system that hosts EnginFrame is mounted with `nosuid` flag unset\. 

The *EF\_SPOOLERDIR directory* is used to hold all the data that's supplied as input and created as output by EnginFrame services\. 

As already mentioned, the spooler directory *must* be accessible by both the EnginFrame Server and EnginFrame Agent\. It must be readable and writable by unprivileged users \(described in the following sections\) and by the `root` user\. 

By default, the spooler directory is placed in a subdirectory of the installation directory\. 

[Managing spoolers](managing-spoolers.md) contains a detailed description of the [system requirements](managing-spoolers.md#spoolers-requirements) for the spoolers directory\. 

## Special users<a name="install-users"></a>

Choose which *system accounts* EnginFrame uses\.

The EnginFrame Administrator is a special system account that has some privileges, such as having access to the EnginFrame Operational Dashboard and some of the configuration files\. This account is referred to as `EF_ADMIN`\. 

Another special account is used to run Tomcat®\. This account is referred to as `EF_NOBODY`\. Make sure that all of the configuration files, along with files in the `$EF_TOP/logs` directory, are owned by `EF_NOBODY` since they might contain sensitive information\. Other users or groups should not be granted permissions to these files\.

Any existing system account *excluding `root`* can be specified\. However, we recommend that you set up two new dedicated users for these roles\. 

In most cases, `efadmin` and `efnobody` are respectively used for `EF_ADMIN` and `EF_NOBODY`\. 

****  
`EF_ADMIN` and `EF_NOBODY` must be operating system valid accounts\. That is, you must be able to log in to the system with those accounts, and they *must not* be disabled\. 

## Authentication<a name="install-authentication"></a>

Last, before installing EnginFrame, select an authentication method to use\. 

EnginFrame can authenticate users using many different mechanisms, including PAM, LDAP, ActiveDirectory, and HTTP Basic Authentication with certificates\. 

If the authentication methods included with EnginFrame don't meet your requirements, you can create your own authentication module\. 

For more information about configuring authentication, see [Authentication framework](chapter-authentication.md)\.

## Digital Rights Management \(DRM\) configuration for Interactive Plugin<a name="interactive-drm-configuration"></a>

The following sections describe the additional requirements for the Interactive Portal\.

**Important**  
EnginFrame periodically checks the status of the interactive jobs using the `EF_ADMIN` user account\.  
This account must be able to access information from all of the Digital Rights Management \(DRM\) mechanisms, such as jobs, files and folder resources\.  
To make sure that this account can access this information, make sure that this account serves as one of your resource manager administrators and has administrator permissions granted\.  
If you don't configure this account accordingly, you might lose some interactive session data\.

**Note**  
When the resource manager controls mixed Windows® clusters, Interactive Plugin submits interactive session jobs on Windows® hosts as the user running EnginFrame Server \(`efnobody` by default\)\. This user must be a valid Windows® user\. 

**Note**  
Starting March 31, 2022, NICE EnginFrame doesn't support VNC®, HP® RGS, VirtualGL, and NICE DCV 2016 and previous versions\.

### IBM® Platform™ LSF®<a name="interactive-drm-configuration-lsf"></a>

Interactive Plugin relies on the LSF® workload manager, to allocate and reserve resources to run the interactive sessions\. Interactive Plugin requires some specific LSF® settings\. 

The following is the configuration steps that are necessary to run Interactive Plugin sessions on your LSF® cluster\. If needed, they can be enhanced or combined with your existing LSF® configuration to achieve more complex resource sharing policies\. 

#### Configuring Queues<a name="interactive-drm-configuration-lsf-configuring-queues"></a>

Interactive Plugin uses resource manager's queues to submit and manage interactive sessions\. You can set up Interactive Plugin to use a default queue and set different services to use different queues\. However, it's important that the queues that are used for any visualization middleware or target system have the following settings: 
+ The EnginFrame Administrator account \(usually `efadmin`\) must be queue administrator of any queue used by Interactive Plugin\.
+ Queues for HP® RGS sessions need to have `HJOB_LIMIT` set to one, since only one HP® RGS session can run on each host\.
+ Queues for HP® RGS Linux® sessions need to have `PRE_EXEC` and `POST_EXEC` respectively set to the `rgs.preexec.sh` and `rgs.postexec.sh` scripts, located under `$EF_TOP/<VERSION>/enginframe/plugins/interactive/tools` folder\.

Here is a configuration snippet for these queues in `lsb.queues`\. You might not need to have all of these queues configured\. You can adapt the parameters as you want, given the preceding requirements\. 

```
Begin Queue
QUEUE_NAME          = int_linux
PRIORITY            = 50
EXCLUSIVE           = y
NEW_JOB_SCHED_DELAY = 0
JOB_ACCEPT_INTERVAL = 0
ADMINISTRATORS      = efadmin
HOSTS               = viz1 vizlin01 vizlin02
DESCRIPTION = Queue for linux interactive applications
End Queue

Begin Queue
QUEUE_NAME          = rgs_linux
PRIORITY            = 50
EXCLUSIVE           = y
NEW_JOB_SCHED_DELAY = 0
JOB_ACCEPT_INTERVAL = 0
HJOB_LIMIT          = 1
ADMINISTRATORS      = efadmin
HOSTS               = viz2 vizlin03 vizlin04
PRE_EXEC = /opt/nice/enginframe/plugins/interactive/tools/rgs.preexec.sh
POST_EXEC = /opt/nice/enginframe/plugins/interactive/tools/rgs.postexec.sh
DESCRIPTION = Queue for RGS linux sessions
End Queue
```

Last, the pre\-run and post\-run scripts for HP® RGS Linux® sessions must run as `root`\. This means that the `/etc/lsf.sudoers` file on all the LSF® nodes must contain the following line: `LSB_PRE_POST_EXEC_USER=root`

**Note**  
Make sure `/etc/lsf.sudoers` is owned by `root` and has permissions 600\. Otherwise, LSF® ignores its contents\.   
After you modify `/etc/lsf.sudoers`, you must run `badmin hrestart all` to restart `sbatchd` on all nodes in the cluster\. 

**Note**  
To specify the default rgs queues inside interactive, edit the `$EF_TOP/conf/plugins/interactive/interactive.efconf` file and add the following two lines\.  

```
INTERACTIVE_DEFAULT_RGS_LINUX_QUEUE=rgs_linux
INTERACTIVE_DEFAULT_RGS_WINDOWS_QUEUE=rgs_windows
```

**Important**  
By default, every pre\-run and post\-run script runs with the credentials of the owner of the job\. After this configuration is applied, all the pre\-execution and post\-execution scripts configured in LSF® at queue level \(`lsb.queues`\) or at application level \(`lsb.applications`\) run with the root account\. The impact on security and functionality must be analyzed case by case\.   
Alternatively, it's also possible to configure the sudo command to run pre\-execution and post\-execution scripts as a normal user with privileges to run as `root` only specific operations\. 

#### Requirements on scheduler tools<a name="interactive-drm-configuration-lsf-requirements"></a>

To operate with interactive sessions on the target operating systems, EnginFrame relies on some tools provided by LSF®\. The scheduler must then be properly configured to make these tools work effectively on the hosts of the cluster\.

The following is a list of LSF® tools that are required by EnginFrame\.
+ Linux® sessions via LSF® require `lsrun`\.

**Important**  
In the recent LSF® versions \(specifically, 9\.1 and later\), the `lsrun` command is disabled by default\. This configuration can be changed by editing file `LSF_TOP/conf/lsf.conf` and setting `LSF_DISABLE_LSRUN=N`\. After this change, the LIM daemon must be asked to reload the configuration, as scheduler administrator running the following command: `lsadmin reconfig` 

### PBS Professional®<a name="interactive-drm-configuration-pbs"></a>

Interactive Plugin relies on the PBS Professional® workload manager, to allocate and reserve resources to run the interactive sessions\. Installation and configuration instructions for PBS Professional® are out of the scope of this document\. However, Interactive Plugin requires some specific PBS Professional® settings\. 

Here is a minimal configuration needed to run Interactive Plugin sessions on your PBS Professional® cluster\. If needed they can be enhanced or combined with your existing PBS Professional® configuration to achieve more complex resource sharing policies\. 

#### Configuring Queues<a name="interactive-drm-configuration-pbs-configuring-queues"></a>

Interactive Plugin uses resource manager's queues to submit and manage interactive sessions\. You can set up Interactive Plugin to use a default queue and set different services to use different queues\. However, it's important that the queues used for any visualization middleware or target system have the following settings: 
+ The EnginFrame Administrator account \(usually `efadmin`\) must be able to see, start, and stop jobs of any queue used by Interactive Plugin\. 
+ You must force the limit of one job per host for HP® RGS queues, because only one HP® RGS session can run on each host\.
+ Queues for HP® RGS Linux® sessions must have `prolog` and an `epilog` respectively set to the `rgs.preexec.sh` and `rgs.postexec.sh` scripts, located under `$EF_TOP/<VERSION>/enginframe/plugins/interactive/tools` folder\. So you might want to copy or link them into `${PBS_HOME}/mom_priv` of each execution host\. 

The following is an example configuration of the `interactive` queue\.

```
# qmgr
Max open servers: 49
Qmgr: create queue interactive
set queue interactive queue_type = Execution
set queue interactive resources_default.arch = linux
set queue interactive enabled = True
set queue interactive started = True
```

### SGE, Son of Grid Engine \(SoGE\), or Univa® Grid Engine® \(UGE\)<a name="interactive-drm-configuration-sge"></a>

Interactive Plugin relies on the SGE workload manager, to allocate and reserve resources to run the interactive sessions\. Installation and configuration instructions for SGE are out of the scope of this document\. However, Interactive Plugin requires some specific SGE settings\. 

Here is a minimal configuration needed to run Interactive Plugin sessions on your SGE cluster\. If needed they can be enhanced or combined with your existing SGE configuration to achieve more complex resource sharing policies\. 

#### Configuring queues<a name="interactive-drm-configuration-sge-configuring-queues"></a>

Interactive Plugin uses resource manager's queues to submit and manage interactive sessions\. You can set up Interactive Plugin to use a default queue and set different services to use different queues\. However, it's important that the queues that are used for any visualization middleware or target system have the following settings\.
+ The EnginFrame Administrator account \(usually `efadmin`\) must be queue administrator of any queue used by Interactive Plugin\.
+ To make the necessary system command line tools and environment available to Interactive Plugin scripts, SGE queues must be configured as follows:
  + The `shell_start_mode` queue parameter has to be set to `unix_behavior`\.
  + If the `shell_start_mode` parameter is set to `posix_compliant`, then the `shell` parameter must be set to `/bin/bash`\.
+ You must force the limit of one job per host for HP® RGS queues, because only one HP® RGS session can run on each host\.
+ Queues for HP® RGS Linux® sessions must have `prolog` and an `epilog` respectively set to the `rgs.preexec.sh` and `rgs.postexec.sh` scripts, located under `$EF_TOP/<VERSION>/enginframe/plugins/interactive/tools` folder\. They must also be run as root, because HP® RGS must operate on runlevels\. Therefore, you might want to have `prolog root@/path/to/enginframe/plugins/interactive/tools/rgs.preexec.sh` in the queue configuration\.

### SLURM™<a name="interactive-drm-configuration-slurm"></a>

 In this scenario, Interactive Plugin relies on SLURM™ Workload Manager to allocate and reserve resources to run the interactive sessions\.

Interactive Plugin requires that features vnc, dcv, dcv2 are defined in the SLURM™ configuration and that every allowed user must be able to check the status and query all SLURM™ jobs and partitions \(alias queues\)\. 'dcv2' stands for DCV since 2017\.

Also, Interactive Plugin requires that the RealMemory \(in MB units\) parameter is defined in the SLURM™ configuration for every execution node to show the correct maximum value of memory\.