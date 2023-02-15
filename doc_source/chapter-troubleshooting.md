# Troubleshooting<a name="chapter-troubleshooting"></a>

## Common issues<a name="common-issues"></a>

 This section lists some common issues and the steps to resolve them:

**Topics**
+ [Breaking change in AJP Connector configuration from EnginFrame 2019\.0\-1424](#breaking-change-ajp-connector-configuration)
+ [Interactive service imports using Slurm before and after EnginFrame version 2020\.1\-r413](#interactive-services-slurm)
+ [Updating to EnginFrame version 2021\.0\-r1646 or later](#hazelcast)
+ [Updating to EnginFrame version 2021\.0\-r1653 or later](#tomcat)
+ [Updating Log4j library in EnginFrame](#log4j-update)

### Breaking change in AJP Connector configuration from EnginFrame 2019\.0\-1424<a name="breaking-change-ajp-connector-configuration"></a>

When updating to 2019\.0\-1424 or later from a previous version, if AJP Connector is enabled, EnginFrame might fail to start after a successful upgrade\. This is because of a breaking change in Tomcat starting from version 7\.0\.100\. From [Tomcat CHANGELOG](https://tomcat.apache.org/tomcat-7.0-doc/changelog.html#Tomcat_7.0.100_(violetagg%29)): 

 * Rename the requiredSecret attribute of the AJP/1\.3 Connector to secret and add a new attribute secretRequired that defaults to true\. When secretRequired is true the AJP/1\.3 Connector will not start unless the secret attribute is configured to a non\-null, non\-zero length String\. * 

By default, Tomcat expects `secret` to be configured\. If you set a `requiredSecret`, it's no longer picked up because of the attribute name change\. To confirm an EnginFrame installation is impacted by this issue, check the `${EF_LOGDIR}/tomcat/catalina.*.log` files for the presence of the following message: 

 * The AJP Connector is configured with secretRequired="true" but the secret attribute is either null or ""\. This combination is not valid\. * 

Resolve the issue in the *$\{EF\_CONF\_ROOT\}/tomcat/conf/server\.xml* file, in the AJP Connector block\. Make one of the following changes and then restart:
+  If you have a non empty *requiredSecret*, rename it to *secret* 
+  Otherwise, add the parameter *secretRequired="false"* 

### Interactive service imports using Slurm before and after EnginFrame version 2020\.1\-r413<a name="interactive-services-slurm"></a>

After the release of EnginFrame version 2020\.1\-r413, you can no longer import interactive services using Slurm as a grid manager with EnginFrame versions that are earlier than 2020\.1\-r413\. To resolve this issue, you must create a new interactive service instead of importing one using Slurm\.

In addition, after 2020\.1\-r413, the default interactive services "Linux Desktop" and "Windows desktop" don't work as\-is when using Slurm as a scheduler\. To make them work, open them in edit mode at least one time\.

### Updating to EnginFrame version 2021\.0\-r1646 or later<a name="hazelcast"></a>

Because Hazelcast is updated by 2 major versions with EnginFrame version 2021\.0\-r1646, you must take additional steps before you update EnginFrame to this and later versions\.

If you have an EnginFrame Enterprise setup, you must first stop the EnginFrame service in all of the instances to perform a successful update to EnginFrame versions 2021\.0\-r1646 or later\.

Moreover, if you have a custom `hazelcast.xml` configuration \(modified from the default configuration\), you must do the following before updating to EnginFrame versions 2021\.0\-r1646 or later:
+ Port the custom `hazelcast.xml` to the format used by Hazelcast 5 following the [relevant Hazelcast documentation](https://docs.hazelcast.com/hazelcast/5.0/migrate/upgrading-from-imdg-3)\.
+ Copy it over to the `$EF_ROOT/conf folder`, overwriting the default `hazelcast.xml` file\.

### Updating to EnginFrame version 2021\.0\-r1653 or later<a name="tomcat"></a>

When performing an update to this version from a previous installation of EnginFrame, you must make sure that the `server.xml` file in the `tomcat` folder `/opt/nice/enginframe/conf/tomcat/conf/server.xml` has this line removed since it breaks Tomcat 9:

```
<Listener className="org.apache.catalina.core.JasperListener"/>
```

If Tomcat is configured to use HTTPS, make sure you remove the `protocol` parameter from the `Connector` section in the `server.xml` config file:

```
<Connector port="{$httpsd_port}" protocol="org.apache.coyote.http11.Http11Protocol"
maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
clientAuth="true" sslProtocol="TLS"
```

should be:

```
<Connector port="{$httpsd_port}"
maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
clientAuth="true" sslProtocol="TLS"
```

### Updating Log4j library in EnginFrame<a name="log4j-update"></a>

Due to an issue in the Apache Log4j library \(CVE: [https://www\.randori\.com/blog/cve\-2021\-44228](https://www.randori.com/blog/cve-2021-44228)\) included in EnginFrame from version 2019\.0\-r1424 to 2021\.0\-r1307, NICE recommends that you upgrade to the latest EnginFrame version available on [https://download\.enginframe\.com](https://download.enginframe.com) or update the Log4j library in your EnginFrame installation as described in the following instructions:

1. Identify the `EF_TOP` and `EF_ROOT` folder of your EnginFrame installation\. For more information, see [Installation directories](planning-deployment.md#installation-paths)\.

1. Identify the log4j files:

   ```
   $ find "$EF_TOP" -name log4j*.jar
   <EF_ROOT>/agent/log4j-core-<OLD_VERSION>.jar
   <EF_ROOT>/agent/log4j-api-<OLD_VERSION>.jar
   <EF_ROOT>/agent/log4j-1.2-api-<OLD_VERSION>.jar
   <EF_ROOT>/WEBAPP/WEB-INF/lib/log4j-core-<OLD_VERSION>.jar
   <EF_ROOT>/WEBAPP/WEB-INF/lib/log4j-api-<OLD_VERSION>.jar
   <EF_ROOT>/WEBAPP/WEB-INF/lib/log4j-1.2-api-<OLD_VERSION>.jar
   ```

   Items highlighted in *red* represent your values\.

1. Stop EnginFrame\. For more information, see [Running NICE EnginFrame](running.md):

   ```
   $  EF_TOP/bin/enginframe stop
   ```

1. Backup the old log4j files to a backup directory of your choice:

   ```
   $ EF_ROOT=...
   BACKUP_AGENT_DIR=/tmp/backup/agent
   BACKUP_SERVER_DIR=/tmp/backup/server
   mkdir -p $BACKUP_AGENT_DIR
   mkdir -p $BACKUP_SERVER_DIR
   mv $EF_ROOT/agent/log4j-core-<OLD_VERSION>.jar $BACKUP_AGENT_DIR
   mv $EF_ROOT/agent/log4j-api-<OLD_VERSION>.jar $BACKUP_AGENT_DIR
   mv $EF_ROOT/agent/log4j-1.2-api-<OLD_VERSION>.jar $BACKUP_AGENT_DIR
   mv $EF_ROOT/WEBAPP/WEB-INF/lib/log4j-core-<OLD_VERSION>.jar $BACKUP_SERVER_DIR
   mv $EF_ROOT/WEBAPP/WEB-INF/lib/log4j-api-<OLD_VERSION>.jar $BACKUP_SERVER_DIR
   mv $EF_ROOT/WEBAPP/WEB-INF/lib/log4j-1.2-api-<OLD_VERSION>.jar $BACKUP_SERVER_DIR
   ```

1. Download and expand the Log4j `tar.gz` you want to update to from [https://logging\.apache\.org/log4j/2\.x/download\.html](https://logging.apache.org/log4j/2.x/download.html)\. It's essential that you verify the integrity of the downloaded files using the PGP and SHA512 signatures, as suggested by the download page of Apache Log4j\.

1. Copy the following jar files from the downloaded package to the EnginFrame folder:

   ```
   $ DOWNLOADED=apache-log4j-<NEW_VERSION>.0-bin
   cp $DOWNLOADED/log4j-core-<NEW_VERSION>.jar $EF_ROOT/agent/
   cp $DOWNLOADED/log4j-api-<NEW_VERSION>.jar $EF_ROOT/agent/
   cp $DOWNLOADED/log4j-1.2-api-<NEW_VERSION>.jar $EF_ROOT/agent/
   cp $DOWNLOADED/log4j-core-<NEW_VERSION>.jar $EF_ROOT/WEBAPP/WEB-INF/lib/
   cp $DOWNLOADED/log4j-api-<NEW_VERSION>.jar $EF_ROOT/WEBAPP/WEB-INF/lib/
   cp $DOWNLOADED/log4j-1.2-api-<NEW_VERSION>.jar $EF_ROOT/WEBAPP/WEB-INF/lib/
   ```

1. Start EnginFrame\. For more information, see [Running NICE EnginFrame](running.md):

   ```
   $ EF_TOP/bin/enginframe start
   ```