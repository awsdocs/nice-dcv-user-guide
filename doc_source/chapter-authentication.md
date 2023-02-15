# Authentication framework<a name="chapter-authentication"></a>

The EnginFrame authentication framework supports a variety of different authentication methods\. You can easily write your own custom mechanism to authenticate users when standard methods don't meet your specific requirements\. 

## Standard EnginFrame authentication authorities<a name="standard-auth-authorities"></a>

When you install EnginFrame, the following built\-in authentication mechanisms are available: 
+ Pluggable authentication modules \(PAM\)
+ Lightweight Delivery Access Protocol \(LDAP\)
+ HTTP authentication
+ Active Directory \(AD\) authentication
+ Certificate\-based authentication

## Default authentication authority<a name="default-authority"></a>

When you install EnginFrame, you choose what authentication method you want to be the default authentication method that's used to access services\. You can change this setting later on\. To change it, change the `EF_DEFAULT_AUTHORITY` property setting in the `server.conf` config file\. For example, to set the default authentication method to PAM, change the relevant line to the following: `EF_DEFAULT_AUTHORITY=pam`\.

The default authentication method that you set when you installed EnginFrame is used by all the services that have the `ef:agent`'s *authority* attribute set to `${EF_DEFAULT_AUTHORITY}`\. This is shown in the following example\.

```
<ef:agent xmlns:ef="http://www.enginframe.com/2000/EnginFrame"
  id="tutorial"
  authority="${EF_DEFAULT_AUTHORITY}">
```

You can set the authentication authority at the `ef:service` level to override the default authentication method that you chose when you installed EnginFrame\. The default authentication authority that you chose is defined in the root `ef:agent` tag\. 

## User mapping<a name="section-user-mapping"></a>

Users can log in to the EnginFrame portal with a username that's different from that of their account in the underlying computing environment, when you configure EnginFrame *user mapping*\. User mapping works by mapping usernames provided at login time to usernames in the underlying operating system\.

For example, the user *John Smith* can log into the EnginFrame Portal using by entering `John Smith` and submit a job that's run as the user `jsmith` on the underlying Unix computing environment\. 

In some cases, user mapping can also be used to map different users of the portal to the same system account, or to map the same user to different accounts on separate systems\. 

**Mapping `root` Account**  
You can't map users to the `root` account\. 

All of the authentication modules that are built\-in and available when you install EnginFrame support user mapping\. 

To enable user mapping, complete the following steps:

1. In the `$EF_TOP/conf/plugins/<authority>/ef.auth.conf` config file, set the `EFAUTH_USERMAPPING` parameter to `true`\.

1. In the `EF_ROOT/plugins/<authority>/bin` directory of the authentication module, add a script that's named `ef.user.mapping`\.

1. Set the ownership of the `ef.user.mapping` file to `root:root` and its permissions to `755` \(`rwxr-xr-x`\)\. 

The `ef.user.mapping` script must output the mapped username for the user that's being authenticated\.

In the following example, `ef.user.mapping` maps all the portal users to the unique `jsmith` user\.

```
#!/bin/sh

echo “jsmith”
```



In the following example, user mapping involves reading a file where each line specifies a mapping using the `Login Name=username` format\. 

For example, a file that's named `EF_ROOT/plugins/<authority>/conf/user.mapping` contains the following\.

```
# simple mapping file
#
# Syntax: loginname=unixaccount
#

Lucy Johnson=ljohnson
John Smith=jsmith
```

In this example, the `ef.user.mapping` script attempts to match the name that's provided by the user during login with the ones that are present on the left\-hand side of the equal sign in the `user.mapping` file\. Then, as shown in the following output, it maps it to the corresponding account name on the right\-hand side of the equal sign\.

```
#!/bin/sh

# read login name from command line
_loginname="$1"

# mapping file
_mappingfile=`dirname "$0"`"/../conf/user.mapping"

# transform login name so it can be used by sed in a safe way
_happysed=`echo "${_loginname}" | sed \
  -e 's#\\\\#\\\\\\\\#g' \
  -e 's#/#\\\\/#g' \
  -e 's/\\./\\\\./g' \
  -e 's/\\[/\\\\[/g'
`
# extract mapped unix account
_mapping=`sed -n 's/^'"${_happysed}"'=\(.*\)$/\1/p' "${_mappingfile}"`

# check with case insensitive flag if necessary
if [ -z "${_mapping}" ] ; then
  _mapping=`sed -n 's/^'"${_happysed}"'=\(.*\)$/\1/pi' "${_mappingfile}"`
fi

# print first result
if [ -n "${_mapping}" ] ; then
  echo "${_mapping}" | sed 'q'
else
  exit 1
fi
```

With user mapping, an administrator can log in as an emulated user that's experiencing issues in a running production environment for testing purposes\. This can be accomplished without compromising other accounts\. With the following simple example `ef.user.mapping` file, a user named `user1` takes on the identity of `user2` without impacting other user accounts\.

```
#!/bin/bash
if [["$1"==user1]] ; then
  echo "user2"
else
  echo "$1"
fi
```

## Configuring the NICE EnginFrame authentication authorities<a name="config-authorities"></a>

Besides the user mapping feature that's described in the previous section, the authentication authorities that are provided when you install EnginFrame have additional configuration parameters that can be changed to tailor the authentication process to your environment\. 

**Topics**
+ [PAM authentication](#config-pam)
+ [LDAP authentication](#config-ldap)
+ [Active Directory authentication](#active-directory)
+ [Using signed certificates with EnginFrame](#config-http)
+ [Certificate authentication](#certificate)

### PAM authentication<a name="config-pam"></a>

The pluggable authentication modules \(PAM\) authority authenticates a user using the PAM method of the Operating System\. 

The `PAM_SERVICE` parameter in the `$EF_TOP/conf/plugins/pam/ef.auth.conf` file on your Agent host specifies which PAM service is used for the authentication\.

### LDAP authentication<a name="config-ldap"></a>

This authority authenticates users querying a LDAP database\. You can configure the settings in the `$EF_TOP/conf/plugins/ldap/ef.auth.conf` config file on your Agent host\. You can specify the location of the LDAP server to use and customize database access\.

The following parameters are available:
+  `LDAP_LDAPSEARCH`: the absolute path to the ldapsearch executable 
+  `LDAP_SERVER`: LDAP Server name or IP address 
+  `LDAP_PORT`: LDAP Server port 
+  `LDAP_BASE`: the base DN \(Distinguished Name\) that's used for the search operation in the LDAP database 

### Active Directory authentication<a name="active-directory"></a>

This authentication authority authenticates users querying an Active Directory database\. You can configure the settings in the `$EF_TOP/conf/plugins/activedirectory/ef.auth.conf` config file on your Agent host\. You can specify the location of the Active Directory server to use and customize database access\. 

The following parameters are available:
+  `AD_LDAPSEARCH`: the absolute path to the ldapsearch executable 
+  `AD_SERVER`: LDAP Server name or IP address 
+  `AD_PORT`: LDAP Server port 
+  `AD_BASE`: the base DN \(Distinguished Name\) for the search operation in the Active Directory database 
+  `AD_BINDAS`: the user that has permissions to bind to an Active Directory Server for queries 
+  `AD_BINDPWD`: the password for a user binding to an Active Directory Server 

### Using signed certificates with EnginFrame<a name="config-http"></a>

HTTP authentication is different from the other EnginFrame authentication methods: HTTP authentication is accomplished by the Web Server\.

After the user is authenticated by the Web Server, the EnginFrame HTTP authentication authority allows you to perform some initialization steps\. Specifically, it allows you to use the EnginFrame user mapping feature that was mentioned in the [User mappingMapping `root` Account](#section-user-mapping) section\. You can use this feature to map the EnginFrame Portal users to the underlying operating system usernames\. 

**Tip**  
When using HTTP authentication, in the case that you need to configure a user mapping that retrieves information from an LDAP Server, we recommend that you use the `openldap` software\.

### Certificate authentication<a name="certificate"></a>

The certificate authority \(CA\) relies on X\.509 certificates to encrypt the channel, check the client's identity, and authenticate users\.

The EnginFrame web server must be configured to use X\.509 certificates for HTTPS channel encryption and client authentication\. EnginFrame uses a certificate authority to authenticate a user\. You can configure either the Apache Tomcat® web server provided with EnginFrame, or an external web server such as Apache® Web Server connected to NICE EnginFrame Tomcat® with AJP connector to use certificates\. For more information, see [Configuring HTTPS](http-ssl.md)\.

For a client to authenticate to EnginFrame, the client must provide a valid certificate the web server recognizes and trusts, and a username to be used by EnginFrame to log in with\.

EnginFrame can be configured to retrieve the username from the first Common Name \(CN\) field of the Distinguished Name \(DN\) certificate property or from the HTTP request parameter named `_username`\.

`authorization.certificate.userCertificate` is that parameter that's used to configure where EnginFrame looks for the client username\. It's in the `server.conf` config file\. If this parameter is set `true`, the username is retrieved from the CN field of the DN in the client certificate\. If this parameter is set to `false`, the username is retrieved from the client HTTP authentication request\. 

With the Certificate authority, like other authentication authorities, it's possible to use the user mapping feature that was mentioned in the [User mappingMapping `root` Account](#section-user-mapping) section\. This allows EnginFrame Portalusers to be mapped to underlying operating system usernames\. 

## Custom authentication authority<a name="custom-authentication-authority"></a>

If none of the standard mechanisms included in EnginFrame meet your specific requirements, you can create your own authentication algorithm\. 

The process of writing a custom EnginFrame authentication module involves the development of the following components: 
+ The `EF_ROOT/plugins/<authority>/etc/<authority>.login` file\. This file is used to specify the fields the users enter for authentication\. Afterwards, the field values are passed to the following authentication module at login time\. 
+ The `EF_ROOT/plugins/<authority>/bin/ef.auth` authentication module script\. It receives the authentication field values that the user entered as input and completes the authentication\.

After the new authority is ready, it can be used in the `authority` attribute for `ef:agent` and `ef:service` tags in the service definition file \(SDF\)\.

**Warning**  
If one of the authentication authorities that's included in EnginFrame doesn't quite meet your specific requirements, *do not modify EnginFrame system files*\. Rather, create your own authority\. You can use the authentication authorities that are provided with EnginFrame as a starting point\.   
It's important to note that modifying one or more of the EnginFrame system files might corrupt the system\. We strongly recommend that you do not modify EnginFrame system files\. Only modify EnginFrame system files at your own risk\. NICE and its partners do not respond for EnginFrame unresponsiveness if a system file has been modified\. Understand also that a future EnginFrame update might override your modifications without warning\. 

### The `<authority>.login` file<a name="authority-login-file"></a>

This XML file defines the authentication parameters that are required by the authentication script to check user credentials\. 

This file specifies the information \(including the username, token, and password\) and prompts for the logon pages that are associated with the authentication module\. 

The login file must match the authority name, that is, the name that will be used in the EnginFrame SDF\. It must also be located under the `EF_ROOT/plugins/<authority>/etc` directory\. For security reasons, the file ownership must be set to `root:root` and its permissions must be `644` \(`rw-r--r--`\)\. 

For example, the login file for authority *PAM* must be: `EF_ROOT/plugins/pam/etc/pam.login` 

The `<authority>.login` file has the following structure: 

```
<ef:login title="login_form_title"
          xmlns:ef="http://www.enginframe.com/2000/EnginFrame">;
  <ef:signature label="login_field_label"
                type="text|password"
                id="authentication_parameter_name" />;
  <!-- [<ef:signature ... />] -->
</ef:login>
```

The following example is taken from the *PAM* authority: 

```
<ef:login title="Login to EnginFrame">
  <ef:signature label="Username: "
                type="text"
                id="_username"/>
  <ef:signature label="Password: "
                type="password"
                id="_password"/>
</ef:login>
```

The `ef:login` entry corresponds to an authentication HTML page\. Referring to the example, the HTML logon page asks users to enter a text token \(the username\) and a password\. 

**Note**  
We strongly recommend that you use the authentication parameters `<ef:signature>` with `id=_username` and `id=_password` \(the `<ef:signature>` tags of the `pam.login` example\)\. Otherwise, you must include `<ef:user\-mapping>` in the `<authority>.login` file to provide the outputs that EnginFrame needs retrieve the username\.

For more information about the XML format that's used by the `<authority>.login` file, see EnginFrame Administrator Reference\. 

### The `ef.auth` File<a name="ef-auth-file"></a>

The script `ef.auth` actually implements the authentication procedure\. 

It must reside under the directory `EF_ROOT/plugins/<authority>/bin`\. The *<authority>* must match the authority name that will be used in the EnginFrame SDF\. For security reasons, the file ownership must be set to `root:root` and its permissions must be set to `755` \(`rwxr-xr-x`\)\. 

For example, the authentication script for the LDAP authority is `EF_ROOT/plugins/ldap/bin/ef.auth`\. 

The authentication script receives as input the login form parameters values that the user entered\. Such values, separated by '`\0`' character \(ASCII code `0`\), are directly passed to the `ef.auth` script in the same order that they're defined in the `<authority>.login` file\. 

Consider the *PAM* authentication authority as an example\. When a user that's named `demo` with a password `secret` logs into EnginFrame, the string `demo\0secret\0` is passed to the `ef.auth` script\. 

The authentication script checks the credentials passed as input and writes the response to the standard output\. If the credential check was successful, the response is as follows: 

```
<?xml version="1.0"?>
<ef:auth xmlns:ef="http://www.enginframe.com/2000/EnginFrame">

  <ef:result>
    <ef:grant />
  </ef:result>

</ef:auth>
```

If it isn't successful, the response is as follows:

```
<?xml version="1.0"?>
<ef:auth xmlns:ef="http://www.enginframe.com/2000/EnginFrame">

  <ef:result>
    <ef:deny />
  </ef:result>

  <ef:error> <!-- Not mandatory -->
    <ef:message>error_message</ef:message>
  </ef:error>

</ef:auth>
```

If the credential check was successful and you have configured user mapping for your custom authentication authority, the `ef:user-mapping` tag is included in the `ef.auth` script output: 

```
<?xml version="1.0"?>
<ef:auth xmlns:ef="http://www.enginframe.com/2000/EnginFrame">

  <ef:result>
    <ef:grant />
    <ef:user-mapping name="target_username"
  </ef:result>

</ef:auth>
```

 `target_username` is the username that's used on the underlying operating system\.

We recommend that you move the user mapping logic to a separate script that can be changed without editing `ef.auth` itself\. The authentication modules that are built into EnginFrame follow the convention of using the `EF_ROOT/plugins/<authority>/bin/ef.user.mapping` script\. For more information, see [User mappingMapping `root` Account](#section-user-mapping)\.

If you move the user mapping logic to a separate script, your `ef.auth` script has the following structure: 

```
[Get credentials]

[Verify credentials]

[If User is authenticated]
   ACTUAL_USERID=[Custom User Mapping procedure]

   [Emit]
       <?xml version="1.0"?>
       <ef:auth xmlns:ef="http://www.enginframe.com/2000/EnginFrame">
         <ef:grant/>
         <ef:user-mapping name="$ACTUAL_USERID"/>
       </ef:auth>
   [end]
[end]
```