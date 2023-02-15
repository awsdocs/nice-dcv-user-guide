# EnginFrame licenses<a name="licenses"></a>

This chapter describes how EnginFrame manages licenses, where license files are located, the meaning of license fields, how license tokens are counted, and how to check EnginFrame's license token usage\. This information is relevant only when running EnginFrame on an on\-premises or non\-EC2 cloud\-based server\. EnginFrame is licensed for free on EC2\. For more information about EnginFrame licensing, see [Obtaining NICE EnginFrame](obtaining.md)\. 

## License file management<a name="section-licenses-files"></a>

EnginFrame loads its license files from `$EF_TOP/license`\. All files ending with `.ef` extension are loaded\.

****  
If you want to replace an EnginFrame license while still retaining your previous license, rename your previous license by changing the `.ef` extension to something else \(for example, add `.OLD` extension to the original file\)\. If you don't make this change, EnginFrame loads the old license\. Having two license for the same EnginFrame component leads to a conflict issue\.

The EnginFrame license management system reads licenses dynamically from the file\-system, and can detect any changes you apply to licenses even to recognize if the license files were added or removed\. 

### Configuring license files location<a name="config-license-files-location"></a>

`$EF_TOP/license` is the default directory where EnginFrame loads licenses from\. This directory can be changed making EnginFrame load licenses from another location in your file\-system\. 

You can modify `EF_LICENSE_PATH` parameter inside `$EF_TOP/conf/enginframe/server.conf`, and then define an absolute file\-system path\. This changes the directory EnginFrame uses to load licenses\. 

Example: `EF_LICENSE_PATH=/mnt/server/ef-licenses` 

## License file format<a name="section-licenses-format"></a>

An EnginFrame license is an XML file that describes one or more EnginFrame licensed components or plugins\. The main component of EnginFrame is `EF Base`\. It activates the core functions of EnginFrame\. 

The license fields are the following:
+ `product`: This field describes the item that's being licensed \(for example, `EnginFrame PRO`\)
+ `release`: A major release of EnginFrame \(for example, 2021\.1\)
+ `format`: The license file format number \(for example, 2\.0\) 
+ `component`: The component that's being licensed\. Example components include `EF Base` and `webservices`\. 
+ `expiration`: The license expiration date\. The value `never` indicates a perpetual license\. 
+ `ip`: The licensed IP addresses where EnginFrame can be deployed\. It can be a single host IP address, a range of IP addresses, or a list of IP addresses\. The license is valid if EnginFrame is running on one of the mentioned hosts IP addresses\. 
+ `type`: The type of license\. Valid values are `DEMO`, `YEAR`, and `FULL`\. 
+ `units`: The number of license tokens\. 
+ `units-per-user`: The number of tokens that EnginFrame locks for each concurrent user\. 
+ `license-hosts`: If this value is set to `true`y, EnginFrame locks a token for each host in the underlying grid infrastructure\. 
+ `hosts-preemption`: If this value is set to `true`, EnginFrame releases tokens that are received by hosts for new users that are accessing the system\. This happens when all tokens have been used\. 
+ `signature`: The license signature that accounts for all the license fields values\. 

The following is an example EnginFrame license\.

```
<?xml version="1.0"?>
<ef-licenses>
  <ef-license-group product="EnginFrame PRO" release="2017.0" format="2.0">
    <ef-license
      component="EF Base"
      vendor="NICE"
      expiration="2017-08-15"
      ip="80.20.156.116"
      licensee="RnD Team"
      type="DEMO"
      units="20"
      units-per-user="1"
      license-hosts="true"
      hosts-preemption="true"
      signature="..." <!-- Omitted for space -->
    />
  </ef-license-group>
</ef-licenses>
```

## License checking<a name="section-licenses-checking"></a>

The most important license fields are `component`, `ip`, `expiration`, and `units`\. You can statically verify the first three fields\. These field values depend on your EnginFrame deployment setup:
+ In the following example of a valid license file format, `component="EF Base"` unlocks the EnginFrame core\. This component is required to unlock other components, such as `webservices`, that can be enabled with a dedicated section in the licence file\.

  ```
  <ef-licenses>
    <ef-license-group product="EnginFrame HPC PRO" release="2021" format="2.0">
      <ef-license
        component="EF Base"
        vendor="NICE"
        expiration="2023-03-31"
        ip="*"
        licensee="nice-enginframe-dev"
        type="DEMO"
        units="30"
        units-per-user="1"
        license-hosts="false"
        hosts-preemption="false"
        signature="------"
      />
      <ef-license
        component="webservices"
        vendor="NICE"
        expiration="2023-03-31"
        ip="*"
        licensee="nice-enginframe-dev"
        type="DEMO"
        units="30"
        signature="------"
      />
  ...
    </-license-group>
  </ef-licenses>
  ```

  Send questions to helpdesk@nice\-software\.com for your requirements and to get help on understanding which components you actually need to satisfy your goals\. 
+ The *IP address* depends on EnginFrame's host\. 
**EnginFrame Server's Host IP Address**  
You must determine EnginFrame Server's host IP address for a valid license\.   
To verify which IP address is correct for the license request, run the `ping `hostname`` command\. This returns the hostname and the IP address information\.   
EnginFrame doesn't allow for loopback IP address, such as `127.0.0.1`\. If you run a ping command and it returns a loopback address, you need to configure the host name resolution for EnginFrame Server\. You can configure it either by editing `/etc/hosts` or by changing the DNS, NIS, or LDAP configurations\. 
+ *Expiration date* states how long your license is valid\. Evaluation licenses last one month\. However, NICE can release licenses with an validity period that meets your evaluation needs\. You can send a request form on the website where you download EnginFrame or send an email to helpdesk@nice\-software\.com\. 
+ The *units* field expresses the total number of license tokens\.

### License token count<a name="section-licenses-tokencount"></a>

Different scenarios have to be considered when EnginFrame counts license tokens\. The scenarios change according to different combinations of some license fields\. 

License tokens are dynamically used by EnginFrame on the base of system usage and load, such as the number of concurrent users or the number of hosts in the grid environment accessed through EnginFrame\. When EnginFrame consumes a token, it subtracts it from the total number of available tokens expressed by the `units` license field\. 

Tokens that are acquired by a user are always released after the user logs out of the system or on his working session expires\. When a user logs out or when a session expires, the user's tokens are released\. Tokens acquired by hosts are released only on pre\-emption \(if expressed in the license, for the needed amount\) or when EnginFrame is restarted \(all tokens are released\)\. 

The following scenarios depict how EnginFrame acquires and releases license tokens:

1. <a name="licenses-scenario1"></a>

   ```
   license-hosts="true"
   hosts-preemption="true"
   ```

   EnginFrame acquires one token for each concurrent user accessing the system and one token for each host in the underlying computing environment\. 

   Because pre\-emption on hosts tokens is switched on, when all the tokens are used, additional users logging into system are granted access by reclaiming one token from those acquired by hosts\. The host whose token has been reclaimed is now unlicensed\. 

   If all tokens are used and there are no more tokens to preempt, system access is denied\. 

   Available tokens are dynamically acquired by users or hosts\. 

   EnginFrame doesn't show unlicensed hosts details, such as the kind of host, status, and memory consumption\.

1. <a name="licenses-scenario2"></a>

   ```
   license-hosts="true"
   hosts-preemption="false"
   ```

   As in the previous scenario, EnginFrame acquires one token for each concurrent user accessing the system and one token for each host in the underlying computing environment\. 

   Differently from the previous scenario, tokens that are used by hosts are never released\. Only restarting EnginFrame resets host's license token status\. 

   When all the tokens are used, the system denies further accesses\. 

   Available tokens are dynamically acquired by users or hosts\. 

   Unlicensed hosts are managed as in the previous scenario\. 

1. 

   ```
   license-hosts="false"
   units-per-user="<n>"
   ```

   In this scenario, EnginFrame acquires `n` tokens for each concurrent user where `n` is a positive integer\. No tokens are acquired by hosts meaning they are all licensed\. 

   This kind of license fits all those cases where you deal with big or growing clusters and it is more convenient to have a flat license for the number of hosts\. 

   When all the tokens are used by users, the system denies further accesses\. If this happens, no token reclaim occurs because host can't acquire new tokens\. 

#### List of licensed hosts<a name="section-licenses-hostlist"></a>

An optional list of licensed hosts for the previous scenarios can be created\. This list spares license tokens though limiting cluster view through EnginFrame\. 

Create `license.hostlist` in `EF_LICENSE_PATH` to declare the list of licensed hosts\. The file must contain the host names, listed one per line\. The host names must be reported in the same way that they are reported by the job scheduler\. 

This following is a `$EF_TOP/license/license.hostlist` example\.

```
host-linux1.nice
host-linux2.nice
host-linux3.nice
host-unix1.nice
host-win1.nice
host-win2.nice
```

## Monitoring license usage<a name="section-license-monitoring"></a>

License token consumption is an important aspect for an EnginFrame administrator\. 

The EnginFrame Operational Dashboard provides administrators with an overview of installed licenses and provide details for used license tokens\. Loaded licenses with their field values are shown as follows\. 

<a name="image-license-details"></a>EnginFrame License Details

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/enginframe/latest/ag/images/admin-guide/ef-license-details.png)

The license token usage details are also provided\.

<a name="image-license-tokens"></a>EnginFrame License Tokens Status

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/enginframe/latest/ag/images/admin-guide/ef-license-tokens.png)

You can monitor the total number of used tokens, which users have logged in, and which hosts are currently licensed\. In the preceding example, EnginFrame acquired a license token for all reported users and hosts\. 

**Note**  
If the same user name connects from two different workstations or browsers at the same time, an extra token is used as a result\. Tokens aren't acquired nominally but on a concurrent user basis only\. 

You can also check if there were any token reclaims in the system previously\. The value reported is the maximum number of reclaimed tokens that occurred since EnginFrame's last restart\. 

<a name="image-license-tokenreclaims"></a>EnginFrame License Tokens Status With Reclaims

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/enginframe/latest/ag/images/admin-guide/ef-license-tokenreclaims.png)

In the preceding screenshot, there are two token reclaims\. In all, there are eight tokens\. All eight tokens were used by six hosts and two users\. The next two requests from `paolo` and `aware` were satisfied but required two token reclaims from the hosts\. 

### Enable debug log messages for licenses<a name="enable-debug-log-messages-for-licenses"></a>

If you're experiencing problems with the EnginFrame license system, require support from the NICE Support Team, or want to check license management details, it is important to enable the license management module's debug log level\. 

You can enable the license module's debug log level by adding a category to the `log.server.xconf` file as shown in the following snippet\.

```
<category name="com.enginframe.common.license" log-level="DEBUG">
  <log-target id-ref="core"/>
</category>
```

Alternatively, use `log.server.verbose.xconf`\. It already has the log level set to `DEBUG`\. 

For more information, see [Customizing logging](logging.md)\. 