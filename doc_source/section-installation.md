# Installing NICE EnginFrame<a name="section-installation"></a>

**Note**  
Starting March 31, 2022, NICE EnginFrame doesn't support VNC®, HP® RGS, VirtualGL, and NICE DCV 2016 and previous versions\.

EnginFrame is distributed with an installer that guides you through how to install it\. The installer is the EnginFrame package itself\. For instruction on how to get your EnginFrame package, see [Downloading EnginFrame](obtaining.md#download-ef)\. 

## Installing<a name="installing-on-unix"></a>

You can use a graphical and a text\-based installer\. If you're installing on machines where you don't have access to an X Window System, we recommend that you use a text\-based installer\.

**Unprivileged User Installation**  
In most cases, we recommend that you install EnginFrame as `root` user\.  
Installation as an unprivileged user is possible, but has the following limitations:  
You can't use authentication mechanisms that require `root` privileges \(for example, PAM\)\.
After the installation, services are run by the user that installed EnginFrame Agent\.

 Make sure that the umask is 022 before launching the installation commands\. 

If Java™ is available in your `PATH`, start the graphical installer as `root` user: 

```
# java -jar enginframe-2021.1.x.y.jar
```

The graphical installer guides you through the installation process\. If the X Window System isn't available, the installer falls back to the text\-based one\. 

Start the user interface of the text\-based installer by specifying `text` argument on the command line interface: 

```
# java -jar enginframe-2021.1.x.y.jar --text
```

The installer shows you the terms of the license agreement\. If you aren't installing EnginFrame on an Amazon EC2 instance, it also prompts you for a valid license file\. If you don't have a valid license file, see [EnginFrame on on\-premises and other cloud\-based servers](obtaining.md#obtain-license-on-prem)\. 

**Note**  
The license file is used to determine if the product type of the EnginFrame installation is *PRO* or *ENT*\. Because EC2 EnginFrame doesn't use a license file, you can determine the product type in one of two ways:  
If you're upgrading from an older installation that used a license file, that license is checked\. The check determines if the installation is *PRO* or *ENT*\. It does this before moving the license file to the backup directory\.
If it's a clean EnginFrame installation, then you're prompted to choose between a *PRO* and *ENT* installation\.
In either case, a field that's called *ef\.product* with the value of *PRO* or *ENT* is written in the `$EF_TOP/conf/enginframe/server.conf` config file\.

The installer prompts you with some questions to tailor the EnginFrame deployment to your needs\. 

After asking all the questions, the installer shows you a summary of your answers\. This is when you can change values before installing\. After summary is accepted, the installer proceeds to set up EnginFrame on current host\. 

**Note**  
When installing using a Java™ Runtime Environment the following warning might appear in the output: `Unable to locate tools.jar. Expected to find it in [...]` This warning is harmless and can be safely ignored\. 

After installation finishes, you can begin to use EnginFrame\. To learn how you can get started with your EnginFrame Portal and test your installation, see [Running NICE EnginFrame](running.md)\. 

A file that's named `efinstall.config` is saved in the directory where you launched the installer from\. This file contains the options that you specified during installation\. This file can be useful to document how you installed EnginFrame\. You can use this information to replicate installation in *batch* mode without requiring user interactions\. 

**Distributed Deployment**  
If you want to run Server and Agent on different hosts, launch the installer on the Server host and select a shared installation directory\. The installer asks if the Server and Agent run on different hosts\. 

### Batch Installation<a name="installing-batch"></a>

When using batch installation, you can replicate an installation on different hosts taking as input a configuration file that's created during a normal install\. To run the EnginFrame installer in batch mode, run the following command\.

```
# java -jar enginframe-2021.1.x.y.jar --batch -f efinstall.config
```

If you didn't specify the `-f` option, the installer searches for a file that's named `efinstall.config` in the current directory\. 

Unless errors occur, EnginFrame installer completes the installation procedure without requiring further user input\. 

## Fine\-tuning your installation<a name="finetuning"></a>

We recommend that you consider fine\-tuning your installation\. You can make adjustments to make sure that your installation of EnginFrame is performing optimally on your system and meets your specific requirements\. 

**Topics**
+ [Spooler download URL](#spooler-download-url)
+ [Optimizing JDK options](#optimizing-jdk-options)
+ [Distributed resource manager options](#distributed-resource-manager-options)
+ [Interactive plugin](#fine-tune-interactive)

### Spooler download URL<a name="spooler-download-url"></a>

The EnginFrame Agent must communicate with EnginFrame Server when downloading a file from a spooler\. In some network configurations and architectures, when a Web Server is placed if front of the EnginFrame Server, this callback URL must be explicitly configured\. 

If you can't download files from your EnginFrame Portal, see [Configure download URL on agent](managing-spoolers.md#spoolers-download-url) for configuring EnginFrame Agent callback URL\. 

### Optimizing JDK options<a name="optimizing-jdk-options"></a>

To fine tune the JVM heap size used to launch the EnginFrame Server or the EnginFrame Agent, you can modify settings in the `$EF_TOP/conf/enginframe.conf` file\. You can set `SERVER_MIN_HEAP` and `SERVER_MAX_HEAP` for the EnginFrame Server, and `AGENT_MIN_HEAP` and `AGENT_MAX_HEAP` for the EnginFrame Agent\.

If you want full control of the JVM options, you can set `SERVER_JAVA_OPTIONS` and `AGENT_JAVA_OPTIONS` in the `$EF_TOP/conf/enginframe.conf` file\. However, note that doing so overrides *all* of the parameters, including the default ones\.

In the following example, the heap size for Agent is set to 1024 MB\.

```
# Initial heap memory size for the EnginFrame Agent
AGENT_MIN_HEAP='1024m'

# Max heap memory size for the EnginFrame Agent
AGENT_MAX_HEAP='1024m'
```

### Distributed resource manager options<a name="distributed-resource-manager-options"></a>

The EnginFrame installer configures the HPC Connector at installation time\. You can modify the HPC Connector parameters in the AWS HPC Connector \(hpc\) main configuration file\. It's located at `$EF_TOP/conf/plugins/hpc/hpc.efconf`\. This is required as a preconfiguration step before HPC Connector can be used within your EnginFrame environment\.
+ `HPCC_AWS_PROFILE_NAME` — The AWS profile name that's used for creating the clusters\.
+ `HPCC_AWS_REGION` — The AWS Region where the clusters will be created by default\.
+ `HPCC_AWS_BUCKET_ARN` — The [Amazon Resource Name \(ARN\)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) of the Amazon S3 bucket that's used for data exchange\.
+ `HPCC_SSM_ROLE_ARN` — The ARN of the IAM role that's used for invoking remote commands using SSM\.
+ `HPCC_S3_ROLE_ARN` — The ARN of the IAM role that's used for data exchange\.
+ `HPCC_PCLUSTER_ROLE_ARN` — The ARN of the IAM role that's used for creating the clusters using AWS ParallelCluster\.
+ `HPCC_USE_INSTANCE_PROFILE` — Set this boolean parameter to `true` if EnginFrame is installed on an Amazon EC2 instance and you want the HPC Connector to use an [ instance profile](https://docs.aws.amazon.com/latest/UserGuide/id_roles_use_switch-role-ec2_instance-profiles.html) instead of the profile mapped to the `ef-iam-user`\. The default value for this parameter is `false`\. For information about how to set up an instance profile, see [Using an IAM role to grant permissions to applications running on Amazon EC2 instances](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html) in the *AWS Identity and Access Management User Guide*\.
+ `HPCC_DELETED_CLUSTER_TTL` the time to live after which a cluster in the deleted state will be removed from the system\. The time span must follow the [ISO8601 duration syntax](https://en.wikipedia.org/wiki/ISO_8601#Durations)\. The default value for this parameter is one day\.
+ `HPCC_COMPLETED_APPLICATION_TTL` the time to live after which a completed remote job is removed from the system\. The time span will need to follow the [ISO8601 duration syntax](https://en.wikipedia.org/wiki/ISO_8601#Durations)\. The default value for this parameter is seven days\.

#### Cluster name label<a name="cluster-name-label"></a>

All the grid plug\-ins in EnginFrame support the option to specify a custom label to be used by the portal to show the name of the clusters\. 

Change the grid plug\-in cluster name by specifying in the plug\-in configuration file the `[PLUGIN-ID]_CLUSTER_LABEL` options:
+ `$EF_TOP/conf/plugins/lsf/ef.lsf.conf`: `LSF_CLUSTER_LABEL=...`
+ `$EF_TOP/conf/plugins/pbs/ef.pbs.conf`: `PBS_CLUSTER_LABEL=...`
+ `$EF_TOP/conf/plugins/sge/ef.sge.conf`: `SGE_CLUSTER_LABEL=...`
+ `$EF_TOP/conf/enginframe/plugins/slurm/ef.slurm.conf`: `SLURM_CLUSTER_LABEL=...`

#### Configuring multiple clusters for the same grid manager<a name="config-multiple-clusters"></a>

Currently, EnginFrame supports the multi\-cluster configuration only for the Slurm plug\-in\. 

Configure multiple Slurm clusters by specifying following options in the plug\-in configuration file `$EF_TOP/conf/enginframe/plugins/slurm/ef.slurm.conf`:
+  `SLURM_CLUSTER_IDS` 

   Comma\-separated list of IDs that are assigned to a cluster\. 
+  `SLURM_CLUSTER_[CLUSTER-ID]_LABEL` 

   \(Optional\) Label to display for the cluster that's identified by the `CLUSTER-ID`\. `CLUSTER-ID` is used if the label isn't set\. 
+  `SLURM_CLUSTER_[CLUSTER-ID]_CONF` 

   For each cluster, the path to the configuration file of the cluster is identified by `CLUSTER-ID`\. 

The following is an example\.

```
# Optional configuration: if not set, only the default cluster will be used,
with following settings:
#SLURM_CLUSTER_LABEL
# (optional, cluster id will be used if not set)

SLURM_CLUSTER_IDS="SLURM1,SLURM2"

# First Cluster
SLURM_CLUSTER_SLURM1_LABEL="SLURM_FIRST"
SLURM_CLUSTER_SLURM1_CONF="/efs/slurm/slurm_121/etc/slurm.conf"

# Second Cluster
SLURM_CLUSTER_SLURM2_LABEL="SLURM_SECOND"
SLURM_CLUSTER_SLURM2_CONF="/efs/slurm/slurm_123/etc/slurm.conf"
```

**Important**  
You can't specify `SLURM_CLUSTER_LABEL` option if multiple Slurm clusters are used\.  
You can only use clusters that are compatible with the Slurm client in the folder indicated by the `SLURM_BINDIR` option\.

### Interactive plugin<a name="fine-tune-interactive"></a>

#### Distributed resource manager<a name="specifying-hpc"></a>

The EnginFrame installer configures the Interactive Plugin depending on the resource manager selection when you install EnginFrame\. If you want to change this setting, the related configuration parameters are located in the Interactive Plugin main configuration file: `$EF_TOP/conf/plugins/interactive/interactive.efconf`\.

The parameters are named `INTERACTIVE_DEFAULT_LINUX_JOBMANAGER` and `INTERACTIVE_DEFAULT_WINDOWS_JOBMANAGER`\. You can set their values to the following:
+ `lsf` \- Sessions are scheduled by LSF® \(*Linux®\-only*\)\.
+ `pbs` \- Sessions are scheduled by PBS Professional® \(*Linux®\-only*\)\.
+ `sge` \- Sessions are scheduled by Sun® Grid Engine, Univa® Grid Engine® \(UGE\) or Son of Grid Engine \(SoGE\) \(*Linux®\-only*\)\.

You can override this behavior on per\-EnginFrame service basis by using `--jobmanager` option of `interactive.submit` session starter script\.

#### Remote visualization technology<a name="specifying-vm"></a>

By default, Interactive Plugin is set to use VNC® remote visualization technology\. If you want to change this setting, the related configuration parameter is located in the Interactive Plugin main configuration file: `$EF_TOP/conf/plugins/interactive/interactive.efconf`\.

The parameter is named `INTERACTIVE_DEFAULT_REMOTE`\. You can set it to one of the following values:
+ `dcv2` \- To manage NICE DCV \(since 2017\.0\) 3D accelerated sessions\.

You can override this behavior on a per\-EnginFrame service basis by using the `--remote` option of the `interactive.submit` session starter script\.

## Installing EnginFrame Enterprise<a name="ef-ent-installation"></a>

**Topics**
+ [Installing a third\-party Load Balancer](#ef-ent-installation-load-balancer)
+ [Setting up the database management system](#dbms-setup)
+ [Configure the EnginFrame service](#ef-service-config)
+ [Start EnginFrame](#ef-start)
+ [Saving database credentials in a keystore](#ef-ent-installation.ef-db-cred-keystore)

### Installing a third\-party Load Balancer<a name="ef-ent-installation-load-balancer"></a>

EnginFrame Enterprise requires a load balancer implementing the *sticky session* strategy\. 

The following sections describe how you can implement load balancing for EnginFrame Enterprise\. This implementation is based on AJP connector and Apache® Web Server frontend with `mod_proxy_balancer` module\. 

**Topics**
+ [Configure the AJP connector](#config-ajp-connector)
+ [Configure the Apache® Proxy](#config-apache-proxy)
+ [Configure the Apache® mod\_proxy\_balancer](#config-apache-mod-proxy-balancer)

#### Configure the AJP connector<a name="config-ajp-connector"></a>

Enable the AJP connector on Tomcat®:
+ Log in as root on the node of the EnginFrame server:

  ```
  # cd $EF_TOP/conf/tomcat/conf
  ```
+ Open the `server.xml` file and add a section to define the AJP 1\.3 connector\.

  ```
  <Connector
    port="8009"
    enableLookups="false"
    redirectPort="8443"
    protocol="AJP/1.3"
    URIEncoding="utf-8" />
  ```

  If port 8009 is used by another application, choose another port\. 

#### Configure the Apache® Proxy<a name="config-apache-proxy"></a>

To enable Reverse Proxy Support in Apache® append the following lines to the main Apache® configuration file \(`APACHE_TOP/conf/httpd.conf`\) and reload the Apache® service\. 

```
<Location "/enginframe">
  DefaultType None
  ProxyPass        ajp://127.0.0.1:8009/enginframe flushpackets=on
  ProxyPassReverse ajp://127.0.0.1:8009/enginframe
</Location>
```

 If your context isn’t `enginframe`, then change the `<Location>` and those two lines accordingly\. 

#### Configure the Apache® mod\_proxy\_balancer<a name="config-apache-mod-proxy-balancer"></a>

This configuration is required to balance the traffic over many EnginFrame instances\. 

Create a specific file \(for example, `ef-ent.conf`\), and add to the Apache® configuration directory\. In most cases, it's `/etc/httpd/conf.d`\. 

The following is an example of the `ef-ent.conf` file content\.

```
Header add Set-Cookie "ROUTEID=.%{BALANCER_WORKER_ROUTE}e;
path=/enginframe" env=BALANCER_ROUTE_CHANGED

<Proxy balancer://enterprise>
  BalancerMember ajp://<ip of EnginFrame Server 1>:8009 route=1
  BalancerMember ajp://<ip of EnginFrame Server 2>:8009 route=2
  ProxySet lbmethod=bybusyness
  ProxySet stickysession=ROUTEID
</Proxy>

<Location "/enginframe">
  ProxyPass        balancer://<enterprise hostname>/enginframe
  ProxyPassReverse balancer://<enterprise hostname>/enginframe
</Location>
```

The `enterprise` alias is an internal parameter\. If necessary, you can change the `enginframe` context\. You must set up the `Header` to store internally the route ID to pass it to `stickysession` variable, useful for automatic management of cookies\. 

### Setting up the database management system<a name="dbms-setup"></a>

An empty database instance that's named `EnginFrameDB` must be created before EnginFrame first startup\. `EnginFrameDB` is case sensitive\. At the first startup, EnginFrame creates all the needed tables\. 

The following sections describe the steps to create the EnginFrameDB database instance on the supported database management system\. 

**Note**  
Don't start an EnginFrame server or servers before the following steps are completed\. 

**Topics**
+ [Install and configure EnginFrame](#config)
+ [Configure the MySQL® database \(version 5\.1\.x and higher\)](#mysql-version)
+ [Configure the Oracle database \(10 and higher\)](#oracle-db-version)
+ [Configure the SQL Server® \(2012, 2008\)](#sql-server)

#### Install and configure EnginFrame<a name="config"></a>

When installing EnginFrame Enterprise, you're asked to insert the JDBC URL to the EnginFrame database instance\. You're also asked to add the username and password that you use to access it\.

```
JDBC URL [default: jdbc:derby://localhost:1527/EnginFrameDB]
> jdbc:mysql://172.16.10.216:3306/EnginFrameDB
Username [default: dbadmin]
> enginframedb
Password
>
```

#### Configure the MySQL® database \(version 5\.1\.x and higher\)<a name="mysql-version"></a>

1. Use the following command on the MySQL® server host to log in as root\.

   ```
   # mysql -p
   ```

1. Create a new database by running the following SQL query for MySQL 5\.x\.

   ```
   # CREATE DATABASE EnginFrameDB;
   ```

   For MySQL 8\.x and later, you must define a character set that isn't UTF8 due to a limitation on row length\.

   ```
   # CREATE DATABASE EnginFrameDB DEFAULT CHARACTER SET latin1;
   ```

1. Create a new user by running the following SQL queries, using single quotes\.

   ```
   # CREATE USER '<username>'@'<host>' IDENTIFIED BY '<password>';
   ```

   Consider the following example\.

   ```
   # CREATE USER 'efdbadmin' IDENTIFIED BY 'efdbpassword';
   # CREATE USER 'efdbadmin'@'%' IDENTIFIED BY 'efdbpassword';
   ```

   The first statement allows access to localhost \(for example, for maintenance actions\)\. In the second line, `'%'` functions as a wildcard that's used to allow all hosts\. You can modify the latest statement to restrict the access to the EnginFrame Servers only\.

1. Grant privileges to the new user on the previously created DB by running the following SQL query\.

   ```
   # GRANT ALL PRIVILEGES ON EnginFrameDB.* TO <username>
     IDENTIFIED BY '<password>';
   ```

   Consider the following example\.

   ```
   # GRANT ALL PRIVILEGES ON EnginFrameDB.* TO 'efdbadmin'
     IDENTIFIED BY 'efdbpassword';
   # GRANT ALL PRIVILEGES ON EnginFrameDB.* TO 'efdbadmin'@'%'
     IDENTIFIED BY 'efdbpassword';
   ```

1. Flush privileges to activate them on the created database:

   ```
   # flush privileges;
   ```

1. Test the connection to the EnginFrameDB database\. From one of the servers where the EnginFrame server instance is installed on, check the connection to the created database using MySQL® client only\.

   ```
   # mysql -h <mysql server hostname/ip address>[:<port>]
       -u <username>
       -p <password>
   ```

   Consider the following example\.

   ```
   # mysql -h mysqlserver -u efdbadmin -p efpassword
   ```

   This message is returned\.

   ```
   Welcome to the MySQL monitor.  Commands end with ; or \g.
   Your MySQL connection id is 87653
   Server version: 5.1.73 Source distribution
   
   Copyright (c) 2000, 2013, Oracle and/or its affiliates. All rights reserved.
   
   Oracle is a registered trademark of Oracle Corporation and/or its
   affiliates. Other names may be trademarks of their respective
   owners.
   
   Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
   
   mysql>
   ```

#### Configure the Oracle database \(10 and higher\)<a name="oracle-db-version"></a>
+ Log in to the database as admin using a SQL client such as the SQuirreL SQL client, using the URI `jdbc:oracle:thin:@<hostname>:<port>:XE` \(for example, `jdbc:oracle:thin:@efentserverdb:1521:XE`\)\.
+ Create a new user by running the following SQL query\.

  ```
  # CREATE USER <username> IDENTIFIED BY <password>>
  ```

  The following is an example\.

  ```
  #  CREATE USER enginframedb IDENTIFIED BY efdbpassword
  ```

  A new schema with name equals to the username is automatically created by the db engine\. Logging into the database with the new user, the user schema is automatically used for that user\.
+ Grant privileges to the new user by running the following SQL query\.

  ```
  # GRANT ALL PRIVILEGES TO <username>
  ```

  The following is an example\.

  ```
  #  GRANT ALL PRIVILEGES TO enginframedb
  ```

  If you need to restrict some privileges for the new user, see the instructions in the [Oracle database documentation](https://docs.oracle.com/en/database/index.html)\. Make sure that the user has both read and write permissions on their schema\. 
+ Change the database user profile to avoid automatic expiration, issuing the following SQL query\.

  ```
  # ALTER PROFILE DEFAULT LIMIT PASSWORD_LIFE_TIME UNLIMITED;
  ```

  This sets the *no password expiration* for all the default user's profile\. 

#### Configure the SQL Server® \(2012, 2008\)<a name="sql-server"></a>
+ Enable TCP/IP networking and remote connections\.
  + Run SQL Server Configuration Manager
  + Go to `SQL Server Network Configuration > Protocols` for SQLEXPRESS
  + Make sure TCP/IP is enabled
  + Open the context menu \(Right\-click\) on TCP/IP and select Properties
  + Verify that, under IP2, the IP address is set to the computer's IP address on the local subnet
  + Scroll down to IPAll
  + Make sure that TCP Dynamic Ports is blank
  + Make sure that TCP Port is set to 1433
+ Create a new database that's named `EnginFrameDB` using the SQL Server Management Studio with default settings\.
+ Create a user with SQL Server® authentication using the SQL Server Management Studio \(for example, create a user with a username that's `enginframedb` and a password that's `efdbpassword` \)\.
  + Make sure the user has at least the `db_owner` role on the EnginFrameDB\. Otherwise, it can't read and create tables\. Check this in the Object Explore\. Go to `Security > Logins`, open a content menu \(right\-click\) on the username and choose `Properties > User Mapping` from the left panel\. 
  + Make sure that both the EnginFrameDB database option and the role membership option are checked \(for example, have both the `db_owner` and `public` options checked\)\.
  + \(optional\) To set EnginFrameDB as the default database for the user, go to `Security > Logins`, open a context menu \(right\-click\) on the username and choose `Properties > General` from the left panel\. 
+ Allow SQL Server® to be accessed through "SQL Server and Windows Authentication mode" and not only through "Windows authentication mode" 
  + Open a context menu \(right\-click\) on the database server instance where EnginFrameDB was created \(for example, SQLEXPRESS\)\.
  + Choose Properties, then Security, Server authentication and choose "SQL Server and Windows Authentication mode"\.

   At this point, EnginFrame must be able to access SQL Server® database and to create tables\. 

### Configure the EnginFrame service<a name="ef-service-config"></a>

The installer can configure the EnginFrame service to start at boot time on the node where it's run\. 

If the installation was performed on a shared file system, log in on each node and run the following command to configure the EnginFrame service to start on all other dedicated nodes\.

```
# $EF_TOP/bin/enginframe host-setup --roles=server,agent --boot=y
```

This configuration starts both server and agent components at node startup\. 

To learn about the `host-setup` options, run the following command\.

```
# $EF_TOP/bin/enginframe host-setup --help
```

### Start EnginFrame<a name="ef-start"></a>

After the EnginFrame service is installed, run the following command to manually start it on every node\.

```
# service enginframe start
```

Check if every database EnginFrameDB instance \(MySQL®, Oracle® or SQL Server®\) has been populated with EnginFrame tables\. 

### Saving database credentials in a keystore<a name="ef-ent-installation.ef-db-cred-keystore"></a>

By default, when you're configure an external database, the database credentials are written to the `server.conf` configuration file\. The option names `ef.db.admin.name` and `ef.db.admin.password` are set to the database username and password\. You can save the database credentials in a keystore instead of the configuration file\.

Setting up the keystore option requires that you edit the `${EF_ROOT}/enginframe/server.conf` file\. The resulting file includes the following contents\.

```
EF_DB_KEY_STORE_ENABLED=true
EF_DB_KEY_STORE=${EF_CONF_ROOT}/enginframe/certs/db.keystore
```

**To migrate the credentials of your external database from the configuration file to the keystore:**

1. Edit the $`{EF_CONF_ROOT}/enginframe/server.conf` file as follows\.

   1. Remove the `ef.db.admin.name` and `ef.db.admin.password` entries\.
**Note**  
Before deleting these entries, make a note of the value that they are set to\. You need them for the following steps\.

   1. Add or modify the `EF_DB_KEY_STORE_ENABLED` entry\. Set it to **true**\.

   1. Add an entry for `EF_DB_KEY_STORE=${EF_CONF_ROOT}/enginframe/certs/db.keystore`\.

1. Run the following command\. 

   `${EF_TOP}/bin/ef-db-credentials.sh --action setDBAdmin --name name --password password`

   Set *name *and *password* to the values that `ef.db.admin.name` and `ef.db.admin.password` were set to in the `${EF_CONF_ROOT}/enginframe/server.conf` file in Step 1\.

1. Restart EnginFrame\. For more information, see [Running NICE EnginFrame](running.md)\.

## Configure EnginFrame to work behind a network proxy<a name="network-proxy-configuration"></a>

Learn how to provide the proxy information EnginFrame needs to route network calls correctly\.

You'll use two java properties:

```
-Dhttp.proxyHost=PROXY HOST
-Dhttp.proxyPort=PROXY PORT
```

If the proxy is configured to work with HTTPS, use:

```
-Dhttps.proxyHost=PROXY HOST
-Dhttps.proxyPort=PROXY PORT
```

**Set the properties in EnginFrame**

1. **Get the java properties that EnginFrame currently uses:**

   1. Run `ps -aux` and locate the EnginFrame process that ends in `org.apache.catalina.startup.Bootstrap start`\.

   1. Copy the line representing the command that launched EnginFrame and copy it to a local bash variable, such as `OPTIONS`:

      ```
      $ OPTIONS="content of copied line"
      OPTIONS_UPDATED=`echo "$OPTIONS" | tr ' ' '\n' | egrep -e '^-D' | tr '\n' ' '`
      ```

      The new variable `OPTIONS_UPDATED` has the content you need to use when you edit the `EnginFrame.conf` file\.

1. **Edit the `EnginFrame.conf` file by adding the variable name `SERVER_JAVA_OPTIONS` to the end of the file and saving it:**

   ```
   # other variables defined
   ...
   SERVER_JAVA_OPTIONS="<values copied from the content of OPTIONS_UPDATED> -Dhttp.proxyHost=$PROXY_HOST -Dhttp.proxyPort=$PROXY_PORT"
   ```

   `PROXY_HOST` and `PROXY_PORT` are placeholders for the proxy host and proxy port\.

1. **Restart the EnginFrame process\.**