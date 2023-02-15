# Obtaining NICE EnginFrame<a name="obtaining"></a>

If you didn't already receive your NICE EnginFrame package from NICE or your EnginFrame reseller, download it from EnginFrame website\. 

## Downloading EnginFrame<a name="download-ef"></a>

EnginFrame packages can be downloaded from the EnginFrame website\. 

[https://www.enginframe.com](https://www.enginframe.com) 

You need a valid account to access the download area\. If you don't have one yet, contact helpdesk@nice\-software\.com or your EnginFrame reseller\. 

## EnginFrame on Amazon EC2<a name="obtain-license-on-ec2"></a>

You don't need a license server to install and use the EnginFrame server on an Amazon EC2 instance\. The EnginFrame server automatically detects that it's running on an Amazon EC2 instance\. It also periodically connects to an Amazon S3 bucket to determine if a valid license is available\. Make sure that your instance can do the following:
+ It can reach the Amazon S3 endpoint\. If it has access to the internet, it connects using the Amazon S3 public endpoint\. If your instance doesn't have access to the internet, configure a gateway endpoint for your VPC with an outbound security group rule\. Alternatively, configure it with an access control list \(ACL\) policy that allows you to reach Amazon S3 through HTTPS\. For more information, see [ Gateway VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-gateway.html) in the Amazon VPC User Guide\. If you experience any issues connecting to the S3 bucket, see [ Why can't I connect to an S3 bucket using a Gateway VPC endpoint?](http://aws.amazon.com/premiumsupport/knowledge-center/connect-s3-vpc-endpoint/) in the AWS Knowledge Center\.
+ It has permission to access the required Amazon S3 object\. Add the following Amazon S3 access policy to the instance's IAM role and replace the Region placeholder \(*region*\) with your AWS Region \(for example, `us-east-1`\)\. For more information, see [Create IAM Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html)\.

  ```
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": "s3:GetObject",
        "Resource": "arn:aws:s3:::enginframe-license.region/*"
      }
    ]
  }
  ```

Access to the instance metadata must be enabled\. By default, it's enabled unless you might have [turned it off](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html)\. You can turn it back on by using the [ modify\-instance\-metadata\-options](https://docs.aws.amazon.com/cli/latest/reference/ec2/modify-instance-metadata-options.html) command\.

If you're installing and using the EnginFrame server on an Amazon EC2 instance, you can skip the rest of this chapter\. The rest of this chapter only applies to using the EnginFrame server on an on\-premises server or one hosted in the cloud\.

## EnginFrame on on\-premises and other cloud\-based servers<a name="obtain-license-on-prem"></a>

When running on an on\-premises server or one hosted in the cloud, you need a valid license to install and run EnginFrame\. If you don't already have one, contact helpdesk@nice\-software\.com or your EnginFrame reseller\. 

EnginFrame licenses are classified as one of the following types:
+ *Demo licenses* — demo licenses aren't bound to any IP address and are valid for one month\. 
+ *Full licenses* — full licenses have time\-unlimited validity and are bound to one or more IP addresses\. 
+ *Year licenses* — year licenses have time\-limited validity and are bound to one or more IP addresses\. 

Contact helpdesk@nice\-software\.com or your EnginFrame reseller to purchase, renew, or update a license\. They can also help you can change your license or obtain a demo license\. 

### Licensed plug\-ins<a name="section-licensed-plugins"></a>

When running EnginFrame on Amazon EC2, a license plugin isn't required\. When running EnginFrame on an on\-premises sever or one hosted in the cloud, plug\-ins require a specific license to work\. The standard plug\-ins that are included in the EnginFrame installation\. This requires that a license have the following characteristics:
+ **interactive** — Enables basic functionalities for Interactive Session management\.
+ **applications** — Enables the Workspace\.
+ **hpc\-support** — Enables the HPC functionalities

Additional plug\-ins provided by NICE might also require a license\.

The license file that's provided by your sales contact in most cases contains license components for all the plug\-ins that are included in your EnginFrame bundle\. 

For more information, check with your NICE sales contact or our support helpdesk@nice\-software\.com\. 

If you have a specific license file, it must be copied under `$EF_TOP/license` folder, and have an *\.ef* extension\. 

It's automatically read by the portal\. You don't need to restart EnginFrame\. 

**Note**  
Remove from the `$EF_TOP/license` folder any older *\.ef* license files that contain expired licenses or licenses that aren't correct\. You want to do this because EnginFrame doesn't accept any license conflict\.

The following is an example license for the *Interactive* component\.

```
<?xml version="1.0"?>

<ef-licenses>
<ef-license-group product="EnginFrame PRO" format="1.0" release="2014.0">
  <ef-license
    component="interactive"
    vendor="NICE"
    expiration="2014-12-31"
    ip="10.20.10.14"
    licensee="Acme.com"
    type="DEMO"
    units="20"
    signature="xxxxxx"
  />
</ef-license-group>
</ef-licenses>
```

For more information about EnginFrame licenses, see [EnginFrame licenses](licenses.md)\. 