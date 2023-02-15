# NICE DCV Session Manager<a name="dcv-session-manager"></a>

NICE DCV Session Manager is a set of installable software packages that includes an Agent and a Broker\. It also includes an API that you can use to build frontend applications that create and manage the lifecycle of NICE DCV sessions across a fleet of NICE DCV servers\.

The NICE DCV Session Manager integration is only supported with NICE DCV 2020\.2 and later\.

Node monitoring, Linux console sessions, autorun files, and sessions screenshots are new features that were introduced in NICE DCV 2021\.0\. These features have been added in EnginFrame 2020\.1 and are only supported by NICE DCV 2021\.0 and later\.

For more information, see [What is NICE DCV Session Manager](https://docs.aws.amazon.com/dcv/latest/sm-admin/what-is-sm.html) in the *NICE DCV Session Manager Administrator Guide*\.

## How to set up NICE DCV Session Manager<a name="installation"></a>

When you [install EnginFrame](planning-deployment.md#remote-visualization-technologies), you can choose to use NICE DCV Session Manager to manage DCV sessions\.

To allow EnginFrame to interact with NICE DCV Session Manager, register EnginFrame as a Session Manager API client\.

If you don't have a client ID and client password for EnginFrame, you must request these credentials from your NICE DCV Session Manager Broker administrator\. For more information about registering your client API with the Broker and obtaining a client ID and password, see [ register\-api\-client](https://docs.aws.amazon.com/dcv/latest/sm-admin/register-api-client.html) in the *NICE DCV Administrator Guide*\.

To properly configure the NICE DCV Session Manager, the installer requires the following information:
+ The base URL of the remote NICE DCV Session Manager\. This URL is used by EnginFrame to manage DCV sessions\. 
+ The full URL, client ID, and client password that EnginFrame uses to authenticate with the Broker\. 

The installer stores this information in the following locations:
+ `$EF_CONF_ROOT/plugins/dcvsm/clusters.props`\. 

  This file contains sensitive information that's used to authenticate to remote NICE DCV Session Managers\. Because of the potential for abuse, this file must have strict permissions\. We recommend that you only grant read and write permissions for the user that is running the Apache Tomcat® server\. Do not make this file accessible to other users\.

  `-rw------- efnobody efnobody`\.
+ `$EF_CONF_ROOT/plugins/dcvsm/dcvsm.efconf`\. 

  This is the configuration file\. It contains the configuration for the NICE DCV Session Manager plugin integration and includes sensitive information\. 

The following is an example `clusters.props` file\.

```
#
# This file has been created during EnginFrame installation.
# It contains only the installation specific settings.
#
# This file contains sensitive data and should be readable by the user running
# EnginFrame but not accessible by others (read/write/execute).
# EnginFrame will refuse to load this file if it is accessible by others.

# Configuration for cluster cl1
DCVSM_CLUSTER_dcvsm_cl1_AUTH_ID=clientID
DCVSM_CLUSTER_dcvsm_cl1_AUTH_PASSWORD=clientPassword
DCVSM_CLUSTER_dcvsm_cl1_AUTH_ENDPOINT=https://sm-hostname:sm-port/oauth2/token
DCVSM_CLUSTER_dcvsm_cl1_SESSION_MANAGER_ENDPOINT=https://sm-hostname:sm-port
DCVSM_CLUSTER_dcvsm_cl1_NO_STRICT_TLS=false
```

The following is an example of the `dcvsm.efconf` file\.

```
# This file has been created during EnginFrame installation.
# It contains only the installation specific settings.
#
DCVSM_CLUSTER_IDS=dcvsm_cl1
```

The name of the cluster that's reported in `DCVSM_CLUSTER_IDS` must match the name that's used for the properties that are described in `clusters.props`\. If this isn't the case, EnginFrame can't retrieve the cluster configuration parameters\. 

## Add more NICE DCV Session Manager clusters<a name="add-clusters"></a>

To add more clusters, you can use the EnginFrame installer\. It creates NICE DCV Session Manager clusters that use a default configuration\. You can change these settings after the cluster is created\.

For each new cluster, the following is required:
+  A new clusterId must be added in `DCVSM_CLUSTER_IDS` \(in a comma separated list\) in `$EF_CONF_ROOT/plugins/dcvsm/dcvsm.efconf`\. 
+  A new set of parameters must be added in `$EF_CONF_ROOT/plugins/dcvsm/clusters.props`\. 

## Enable hosts monitoring for NICE DCV Session Manager<a name="hosts-monitoring"></a>

By default, NICE DCV Session Manager hosts are not shown in the *Hosts* section of the portal\. To enable this feature, edit two configuration files to meet the following requirements: 
+ The `dcvsm` string must be added in `EF_GRID_MANAGERS` \(comma separated list\) in `$EF_CONF_ROOT/plugins/grid/grid.conf`\. 
+ The `dcvsm` string must be added in `GRID_XML_PLUGINS` \(comma separated list\) in `$EF_ROOT/plugins/grid/conf/jobcache.efconf`\. 

 After you change these properties, you must restart EnginFrame to apply the changes\. 

## NICE DCV Session Manager secure connection configuration<a name="tls-configuration"></a>

By default, the installer configures a secure connection using strict TLS checking between EnginFrame and the NICE DCV Session Manager Broker\. We recommend that you use this default configuration\. 

If you so choose, you can disable this behavior by setting `DCVSM_CLUSTER_clusterID_NO_STRICT_TLS` to `true` in the `clusters.props` configuration file\. 

If a valid certificate is presented, EnginFrame trusts the DCV Session Manager Broker\. 

If the NICE DCV Session Manager Broker is configured to use self\-signed certificates, make sure that the root certificate is added to the Tomcat JVM KeyStore\. 

### <a name="tls-add-root-certificate-to-keystore"></a>

For instructions on how to add a root certificate to the Tomcat JVM KeyStore, see [Configuring HTTPS](http-ssl.md)\. 

In the following example, the `CA_ROOT.pem` file that's provided by the NICE DCV Session Manager Broker is used\.

```
# 1. export the Session Manager CA Certificate in der format with openssl
openssl x509 -in CA_ROOT.pem -inform pem -out ca.der -outform der

# 2. Verify that Java Keytool is able to read the certificate
keytool -v -printcert -file ca.der

# 3. import Session Manager CA Certificate in JVM keytool
keytool -importcert -alias dcvsm \
        -keystore $JAVA_HOME/lib/security/cacerts \
        -storepass java_keystore_password \
        -file ca.der

# 4. verify that the root certificate has been imported
keytool -keystore "$JAVA_HOME/lib/security/cacerts" \
        -storepass java_keystore_password \
        -list | grep dcvsm
```

## How to create a new remote desktop interactive service<a name="create-service"></a>

An Admin user can create a new remote interactive service using NICE DCV Session Manager from the Virtual Desktop portal\. 

A NICE DCV Session Manager cluster supports both Windows and Linux hosts\.

### Session modes<a name="session-placement"></a>

The [interactive plugin](planning-deployment.md#interactive-requirements) with NICE DCV Session Manager, creates `VIRTUAL` or `CONSOLE` sessions in Linux hosts and `CONSOLE` sessions in Windows hosts\. For more information about session types and support, see [NICE DCV Session Manager documentation](https://docs.aws.amazon.com/dcv/#nice-dcv-session-manager)\.

`CONSOLE` sessions support one or more session per instance\. This is the default for Windows hosts\. You can create a maximum of 3 Windows sessions because there only 3 instances deployed\.

`VIRTUAL` sessions support only one sessions per instance\. This is the default for Linux hosts\.

**Important**  
`VIRTUAL` and `CONSOLE` sessions can't be active on the same host at the same time\.

### Create a remote desktop interactive service<a name="create-interactive-service"></a>

Create and publish a remote desktop interactive service

1. Open the EnginFrame portal and **Login** as Admin user\.

1. Choose the **Virtual Desktop**\.

1. Choose **Switch to Admin View** in the header navigation pane\.

1. In the sidebar navigation pane, choose **Manage** and then **Interactive Services**\.

1. Choose **New** to create an interactive service\.

1. Select **Create from Template** and choose **Create**\.

1. Choose **Settings**\. Here you can customize your service\. Choose **Close** to skip to the next step\.

1. In the yellow box, type in a new name for your service, such as "MyService"\.

1. Choose **Launch Session**\.

1. Review and keep the settings, including the **Session Mode** in the **Execution Environment** section\.

1. Choose **Close**, **Save**, and **Close**\.

1. To modify or test the service, select your new service and choose **Edit**\.

1. To publish the service, select your new service and choose **Publish**, then select **All Users** and **Publish**\.

1. Choose **Switch to User View** in the header navigation pane\.

1. Your new remote interactive service is displayed under **Services** and available for use\.

Using NICE DCV Session Manager, you can tag the host where the DCV Server is running with custom values\. You can also use these values to select which host the session is created on\. For more information, see the [NICE DCV Session Manager documentation](https://docs.aws.amazon.com/dcv/latest/sm-admin/what-is-sm.html)\.

With EnginFrame session placement, you can create an interactive service that targets hosts with specific characteristics\. Using this feature, you don't need to recall specific details such as the hostname or IP address and delegate their discovery to the remote NICE DCV Session Manager Broker\. 

To specify a set of "tags" for targeting the host, add the `submitopts` option in the `ActionScript` tab:

```
vdi.launch.session --submitopts " ram_gb='4' Software='My Software' "
```
+ Multiple tags can be specified, separated by spaces\. 
+ Each tag is a key\-value pair that's in the format of "key=value"\. There can't be any spaces before and after the equal sign \(=\) unless the keys and values are wrapped in single quotes \('\)\.

If no hosts are available, the session fails to be created\. This can happen if there is no hosts or if all the hosts are in use and aren't available to create the session\.

EnginFrame 2020\.1\+ provides the possibility to specify a custom `Autorun File` to be run when a session is created\. The file must be present on the remote host within a reserved folder\. For more information about autorun files, see [NICE DCV Session Manager documentation](https://docs.aws.amazon.com/dcv/#nice-dcv-session-manager)\.

This feature is only compatible with NICE DCV Session Manager 2021\.0\+ on `CONSOLE` sessions on Windows NICE DCV servers and `VIRTUAL` sessions on Linux NICE DCV servers\. It is not supported with `CONSOLE` sessions on Linux NICE DCV servers\.

To specify the `Autorun File`, add the `delegate-autorun-file` option in the `ActionScript` tab\. You can do this by running the following command\.

```
vdi.launch.session --delegate-autorun-file "autorun/relative/file/path.sh"
```

## Plugin limitations<a name="limitations"></a>

Custom `Init Script`s aren't supported\. Linux virtual sessions use the default scripts that are provided by NICE DCV\.

Sessions can be shared only with `Collaborators`\. There is currently no support for sharing with `Viewers`\.

## Troubleshooting<a name="troubleshooting"></a>

### Compatibility with NICE DCV versions<a name="troubleshooting-compatibility-with-nice-dcv"></a>

EnginFrame 2020\.1 added several new features\. These included node monitoring, Linux console sessions, autorun files, and session screenshots\. These features only work with NICE DCV 2021\.0 and later\. They do not work with earlier versions\. To use these features and avoid issues of incompatibility, upgrade to a compatible version\.

If you try to use these features with an earlier version, an error like the following might occur\.

```
SMClient.getSessionScreenshot: If you are not using DCVSM 2021.0+,
    please be aware that getSessionScreenshot is not supported.
    Protocol version: 2020.2
```

### Log files<a name="troubleshooting-logfiles"></a>

The main NICE DCV Session Manager plugin log file is located under the EnginFrame log directory that's named `${EF_LOGDIR}/dcvsm.log`\. 