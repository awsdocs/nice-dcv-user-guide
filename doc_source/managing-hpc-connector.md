# Managing AWS HPC Connector<a name="managing-hpc-connector"></a>

HPC Connector requires [AWS CLI version 2](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) and AWS ParallelCluster 3\.0\.2 or later to be pre\-installed on the node that's running the EnginFrame server\. This means that the user `efnobody` running the EnginFrame Server must have access to the package and permissions to run the `pcluster` command\.

Before you install EnginFrame, make sure that AWS ParallelCluster is installed by running the following command as the user `efnobody` that is running the EnginFrame server\.

```
$ pcluster version
```

The output is as follows:

```
{
  "version": "3.0.2"
}
```

For instructions on how to set up and configure AWS ParallelCluster, see the [AWS ParallelCluster guide](https://docs.aws.amazon.com/parallelcluster/latest/ug/install-v3-virtual-environment.html)\. This setup includes setting up required dependencies\. Among these dependencies, NodeJS must be accessible to the user `efnobody` that's running the EnginFrame server\.

We recommend that you install AWS ParallelCluster in a Python virtual environment\. This avoids requirement version conflicts with other Python packages\.

## Activating an AWS ParallelCluster virtual environment<a name="activating-pcluster-virtual-env"></a>

You must reactivate the virtual environment with every restart\. As a result, we recommended that you add it in your `init` environment file \(for example, `~/.bashrc`\) for the user\.

```
source [YOUR_VIRT_ENV_PATH]/bin/activate
```

## Before installing EnginFrame with AWS HPC Connector<a name="before-installing-enginframe"></a>

To start HPC Connector, the EnginFrame installer requires the following parameters:
+ An AWS Region where the cluster is created and managed\.
+ An Amazon S3 bucket to transfer data between EnginFrame and the remote clusters\.
+ Three IAM roles that are used to access data on the S3 bucket, submit jobs using SSM, and manage clusters using AWS ParallelCluster\.
+ An AWS instance profile or an AWS profile name containing AWS credentials for an \(`<ef-iam-user>`\) able to assume the roles\.

To simplify the setup of these resources, you can use a deployment script to create the required resources on your AWS account\. Select one of the following links to bootstrap AWS HPC Connector\.
+ [US East \(N\. Virginia\) Region](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)
+ [US East \(Ohio\) Region](https://console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)
+ [US West \(N\. California\) Region](https://console.aws.amazon.com/cloudformation/home?region=us-west-1#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)
+ [US West \(Oregon\) Region](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)
+ [Canada \(Central\) Region](https://console.aws.amazon.com/cloudformation/home?region=ca-central-1#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)
+ [Europe \(Frankfurt\) Region](https://console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)
+ [Europe \(Ireland\) Region](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)
+ [Europe \(Stockholm\) Region](https://console.aws.amazon.com/cloudformation/home?region=eu-north-1#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)
+ [Europe \(Milan\) Region](https://console.aws.amazon.com/cloudformation/home?region=eu-south-1#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)
+ [Asia Pacific \(Tokyo\) Region](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)
+ [Asia Pacific \(Seoul\) Region](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-2#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)
+ [Asia Pacific \(Hong Kong\) Region](https://console.aws.amazon.com/cloudformation/home?region=ap-east-1#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)
+ [Asia Pacific \(Mumbai\) Region](https://console.aws.amazon.com/cloudformation/home?region=ap-south-1#/stacks/quickcreate?templateUrl=https%3A%2F%2Fnice-enginframe-download-us-east-1.s3.amazonaws.com%2Fenginframe%2Ftemplates%2FAWS-HPC-Connector.yaml&stackName=hpc-connector)

## AWS credentials and profile<a name="credentials-profile"></a>

HPC Connector requires users to have a valid set of credentials for `<ef-iam-user>` that are stored in the `.aws/credentials` file of the user `efnobody` that's running the EnginFrame server\. Make sure that the credential file has an entry that's similar to the following example\.

```
[<profile-name>]
aws_access_key_id=<aws access key for the account>
aws_secret_access_key=<aws secret access for the account>
```

EnginFrame assumes that this credential file is already present at installation time, and that a profile with the name that's provided during setup is already present\. It asks for the profile name that's used for creating the clusters, and performs a check on the credentials file\. If no file is present or if a profile with the given profile name is not present, the installer logs a warning and continues its operation, assuming that the profile will be created at a later time\.

## Amazon S3 bucket for data transfer<a name="s3-bucket-enginframe"></a>

When launching a job on a cluster running on AWS, HPC Connector uses an Amazon S3 bucket to transfer input and output data to from the remote folder where the job is to run\. To use the Amazon S3 bucket, you must provide the Amazon resource name \(ARN\) of the S3 bucket when using the EnginFrame installer\.

**Warning**  
In general, the overall size of a file that's transferred for a single job doesn't need to exceed 100MB\. If the overall file size exceeds 100MB, the system might time out on the transfer operation, and the job or copy might fail\. If your jobs need to access larger datasets, make sure that these are available to the cluster through a shared file system\. For more information about how to mount shared storage, see [Shared storage](https://docs.aws.amazon.com/parallelcluster/latest/ug/SharedStorage-v3.html) in the AWS ParallelCluster User Guide\.
HPC Connector doesn't support [Using Amazon S3 bucket keys](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-key.html)\.

## HPC Connector IAM roles<a name="hpc-connector-iam-roles"></a>

AWS HPC Connector uses AWS Identity and Access Management \(IAM\) roles to control permissions that are associated with the AWS resources that are deployed to a selected AWS account\. HPC Connector runs multiple operations on the selected AWS account\. It creates and manages clusters using AWS ParallelCluster commands\. It also submits and manages jobs on remote clusters, and transfers input and output data between clusters and the EnginFrame spoolers\. HPC Connector uses different roles to limit the scope to the minimum permissions required for each operation\.
+ An IAM role for managing AWS ParallelCluster \(`ef-parallelcluster-role`\) in your account\. This role is used by HPC Connector for creating, starting, and stopping clusters\. It must have AWS ParallelCluster’s policies attached for managing the clusters\.
+ An IAM role for accessing the Amazon S3 bucket \(`ef-s3-role`\)\. This is used by HPC Connector for transferring the data back and forth from the remote destination\. This role has a policy \(`ef-s3-role-policy`\) that's attached for accessing the Amazon S3 bucket and reading or writing objects\.
+ An IAM role for running jobs remotely using SSM \(`ef-ssm-role`\)\. This is used for launching job scripts remotely on the clusters\. This role has a policy \(`ef-ssm-role-policy`\) that's attached for sending commands to the remote instances\.

You can create IAM policies and roles to control the permissions that are granted to HPC Connector and to the users of the cluster\. The following examples show the IAM policies and roles that are required to use HPC Connector\. In the policies, replace `aws-account-id` and similar strings with the appropriate values\.

**Note**  
The following examples include Amazon Resource Names \(ARNs\) for the resources\. If you're working in the AWS GovCloud \(US\) or AWS China partitions, the ARNs must be changed\. Specifically, they must be changed from "arn:aws" to "arn:aws\-us\-gov" for the AWS GovCloud \(US\) partition or "arn:aws\-cn" for the AWS China partition\. For more information, see [Amazon Resource Names \(ARNs\) in AWS GovCloud \(US\) Regions](https://docs.aws.amazon.com/govcloud-us/latest/UserGuide/using-govcloud-arns.html) in the *AWS GovCloud \(US\) User Guide* and [ARNs for AWS services in China](https://docs.amazonaws.cn/aws/latest/userguide/ARNs.html) in *Getting Started with AWS services in China*\.

AWS ParallelCluster IAM policy and role  
HPC Connector uses AWS ParallelCluster to provision clusters and must have access to both the [Base user policy required to invoke AWS ParallelCluster features](https://docs.aws.amazon.com/parallelcluster/latest/ug/iam-roles-in-parallelcluster-v3.html#iam-roles-in-parallelcluster-v3-base-user-policy) and the policy for [Privileged IAM access mode](https://docs.aws.amazon.com/parallelcluster/latest/ug/iam-roles-in-parallelcluster-v3.html#iam-roles-in-parallelcluster-v3-privileged-iam-access)\.  
For more information how to create the policy, see [AWS Identity and Access Management roles in AWS ParallelCluster 3\.x](https://docs.aws.amazon.com/parallelcluster/latest/ug/iam-roles-in-parallelcluster-v3.html)\.  
The AWS ParallelCluster IAM role then needs to be configured with the following trust relationship to allow EnginFrame to use it:  

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<aws-account-id>:user/<ef-iam-user>"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

SSM IAM policy and role  
The following policy shows the permissions that are required by HPC Connector to run SSM commands for managing jobs\.   

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ssm:SendCommand"
            ],
            "Resource": [
                "arn:aws:ec2::<aws-account-id>:instance/*"
            ],
            "Condition": {
                "StringLike": {
                    "ssm:resourceTag/parallelcluster:node-type": ["HeadNode"]
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "ssm:SendCommand"
            ],
            "Resource": [
                "arn:aws:ssm:::document/AWS-RunShellScript"
            ]
        },
        {
            "Action": [
                "ssm:GetCommandInvocation"
            ],
            "Effect": "Allow",
            "Resource": "*"
        }
    ]
}
```
Create the policy, assign it a name \(`ef-ssm-role-policy`\) and attach it to an IAM role \(for example, `ef-ssm-role`\)\. The policy requires all the instances to have a specific tag that's assigned automatically by AWS ParallelCluster to head nodes\. This prevents arbitrary SSM commands from running on instances that aren't head nodes\. Then configure it with the following trust relationship to allow EnginFrame to use it:   

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<aws-account-id>:user/<ef-iam-user>"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

Amazon S3 IAM policy and role  
The following policy shows the permissions that are required by HPC Connector to move files between the EnginFrame node and remote spoolers using Amazon S3\. Replace `<s3-bucket>` with the actual Amazon S3 bucket name\.  

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::<s3-bucket>"
            ],
            "Effect": "Allow"
        },
        {
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject"
            ],
            "Resource": [
                "arn:aws:s3:::<s3-bucket>/*"
            ],
            "Effect": "Allow"
        }
    ]
}
```
Create the policy, assign it a name \(for example, `ef-s3-role-policy`\), and attach it to an IAM Role \(`ef-s3-role`\)\. Then configure it with the following trust relationship to allow EnginFrame to use it:   

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
        "Effect": "Allow",
        "Principal": {
            "AWS": "arn:aws:iam::<aws-account-id>:user/<ef-iam-user>"
        },
        "Action": "sts:AssumeRole"
    }
  ]
}
```
Access to the Amazon S3 bucket is required only by the head nodes of the remote clusters\. Therefore, you must add a condition that limits the access only to the instance policies that are created by AWS ParallelCluster\. This can be done by specifying a condition on the IAM role \(`ef-s3-role`\)\.  

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
        "Effect": "Allow",
        "Principal": {
            "AWS": "arn:aws:iam::<aws-account-id>:root"
        },
        "Action": "sts:AssumeRole",
        "Condition": {
            "StringLike": {
            "AWS:PrincipalArn": "arn:aws:iam::<aws-account-id>:role/parallelcluster/*" 
            }
        }
    }
  ]
}
```

EnginFrame   
An `<ef-iam-user>` must be configured with the following policy that allows it to assume the previously defined AWS ParallelCluster, Amazon S3, and SSM roles\.  

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": "sts:AssumeRole",
            "Resource": "arn:aws:iam::<aws-account-id>:role/<ef-parallelcluster-role>",
            "Effect": "Allow"
        },
        {
            "Action": "sts:AssumeRole",
            "Resource": "arn:aws:iam::<aws-account-id>:role/<ef-s3-role>",
            "Effect": "Allow"
        },
        {
            "Action": "sts:AssumeRole",
            "Resource": "arn:aws:iam::<aws-account-id>:role/<ef-ssm-role>",
            "Effect": "Allow"
        }
    ]
}
```

## AWS ParallelCluster configuration requirements<a name="parallelcluster-cluster-config"></a>

**Topics**
+ [Required additional IAM policies](#required-iam-policies)
+ [AWS ParallelCluster head node policy](#parallelcluster-head-node-policy)
+ [Scoping down HPC Connector](#scoping-down-hpc-connector)
+ [Managing clusters](#managing-clusters)
+ [Managing jobs](#managing-jobs)

### Required additional IAM policies<a name="required-iam-policies"></a>

AWS HPC Connector requires AWS ParallelCluster configurations to have specific additional policies attached to the IAM role used for the head node\. Most specifically, as the job submission uses SSM, the `AmazonSSMManagedInstanceCore` must be attached to the additional policies\. In addition to SSM, the head node must also assume the role that's needed by HPC Connector to transfer the files back and forth\.

### AWS ParallelCluster head node policy<a name="parallelcluster-head-node-policy"></a>

AWS ParallelCluster configurations must include a role policy for the cluster head node \(`parallelcluster-ef-instance-policy`\) to allow data transfer to and from the regional Amazon S3 bucket\. Be aware that the name of the policy must start with the parallelcluster prefix in order for it to be attached to the head node\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": "sts:AssumeRole",
            "Resource": "arn:aws:iam::<AWS ACCOUT ID>:role/<ef-s3-role>",
            "Effect": "Allow"
        }
    ]
}
```

The policies \(both the head node policy and the SSM managed instance core policy\) must be present in your configuration in order for the cluster to be managed by HPC Connector

```
HeadNode:
  Iam:
    AdditionalIamPolicies: 
     - Policy: arn:aws:iam::aws:policy/AmazonSSMManagedInstanceCore 
     - Policy: arn:aws:iam::<account-id>:policy/<parallelcluster-ef-instance-policy>
```

### Scoping down HPC Connector<a name="scoping-down-hpc-connector"></a>

HPC Connector allows running SSM commands only to head nodes\. It does this by using the `parallelcluster:node-type` tag added automatically by AWS ParallelCluster when it provisions a new head node instance\. This restriction is specified in the SSM policy that is required by HPC Connector to work properly\. However, the default policy HPC Connector can access any head node, even if it wasn't created specifically by HPC Connector itself\. This can be further scoped down by specifying a different tag name and value in the SSM policy \(`ef-ssm-role-policy`\) and having AWS ParallelCluster set that tag on the head node by adding a Tags section in the configuration file\. For instance, for setting a tag named `ef:instance` to the remote value, the following section can be added in AWS ParallelCluster’s configuration file\.

```
Tags:
  -Key: ef:instance
  Value: remote
```

### Managing clusters<a name="managing-clusters"></a>

The management of clusters in EnginFrame is performed within two distinct views that are available in the Admin View section of EnginFrame\.
+ The AWS Cluster Configurations view, which manages AWS ParallelCluster configurations\.
+ The Clusters view, which shows all of the running clusters accessible by EnginFrame\.

#### AWS Cluster Configurations page<a name="cluster-config-view"></a>

The AWS Cluster Configurations page displays all the AWS ParallelCluster configurations that administrators have imported in EnginFrame\. The configurations define all the properties of a cluster on AWS, including queues, compute resources, and shared storage\. HPC Connector only supports AWS ParallelCluster 3 template files as cluster configurations\. In this view administrators can register new cluster configurations, rename and delete them, and launch new clusters based on that configuration\. The following sections will provide instructions on how to operate on the AWS Cluster Configurations page\.

##### List the AWS Cluster Configurations<a name="list-the-cluster-config"></a>

1. Log in to the Workspace as a user with administrator privileges\.

1. To open the Admin view, on the top\-right corner choose **Switch to Admin View**\.

1. Under the **Manage** section in the left menu, select **AWS Cluster Configurations**\.

##### Register an AWS Cluster Configuration<a name="register-cluster-config"></a>

**Note**  
Before registering an AWS ParallelCluster configuration, make sure it complies with the HPC Connector requirements\. For more information, see [AWS ParallelCluster configuration requirements](#parallelcluster-cluster-config)\.

1. Log in to the Workspace as a user with administrator privileges\.

1. To open the Admin’s portal, on the top\-right corner choose **Switch to Admin View**\.

1. Under the **Manage** section in the left menu, select **AWS Cluster Configurations**\.

   The list of the cluster configurations is displayed in the table\. 

1. Choose **Register** at the top of the table\.

1. In the **Register Cluster Configuration** box, fill in the fields:
   + **AWS ParallelCluster configuration** — Choose between “Upload file” and “Paste text”
   + **Upload file** — Select a valid AWS ParallelCluster configuration file
   + **Paste text** — Enter a valid AWS ParallelCluster configuration file in the textbox\.

1. Choose **Register**\.

##### Rename an AWS Cluster Configuration<a name="rename-the-cluster-config"></a>
+ Log in to the Workspace as a user with administrator privileges\.
+ To open the Admin’s portal, on the top\-right corner choose **Switch to Admin View**\.
+ Under the **Manage** section in the left menu, select **AWS Cluster Configurations**\.

  The list of the cluster configurations is displayed in the table\. 
+ Select the **Actions** drop\-down menu on your chosen configuration\.
+ Choose **Rename**\.
+ Add the new configuration name\.
+ Choose **Rename** to submit the new name\. The new name will be visible in the configuration list after a few moments\.

##### Delete an AWS Cluster Configuration<a name="delete-the-cluster-config"></a>
+ Log in to the Workspace as a user with administrator privileges\.
+ To open the Admin’s portal, on the top\-right corner choose **Switch to Admin View**\.
+ Under the **Manage** section in the left menu, select **AWS Cluster Configurations**\.

  The list of the cluster configurations is displayed in the table\. 
+ Select the **Actions** menu on your chosen configuration\.
+ Choose **Delete** action from the dropdown\.
+ Choose **OK** to confirm deletion\. The configuration will be removed from the configuration list after a few moments\.

##### Start a new cluster from an AWS Cluster Configuration<a name="start-the-cluster-config"></a>
+ Log in to the Workspace as a user with administrator privileges\.
+ To open the Admin’s portal, on the top\-right corner choose **Switch to Admin View**\.
+ Under the **Manage** section in the left menu, select **AWS Cluster Configurations**\.

  The list of the cluster configurations is displayed in the table\. 
+ Select the **Actions** menu on your chosen configuration\.
+ Choose **Create Cluster** action from the menu\.
+ Enter the **Cluster Name** field with your preferred cluster name\.
+ For **User Mode**, choose **Single user** or **Multi User 1:1**\.
+ Choose **Create** to submit the cluster creation\.
+ Creating the new cluster might require a few minutes\. During that time, the state of the cluster in the cluster list page will change upon refresh\. When a cluster is ready to be used its status will transition to **Ready** on the **Clusters ** page\.

#### Clusters page<a name="clusters-page"></a>

The Clusters view contains all the clusters from all the grid managers that are linked to EnginFrame\. For each cluster, we show the name, the scheduler, the type \(Local or AWS Cloud\), the list of available queues, and the cluster status\. Only clusters with the status Ready can serve traffic and be used for job submission\.

By choosing the **Actions** arrow that appears hovering on a row, some functionalities are shown on clusters with type AWS Cloud\. Depending on the state of the cluster, you can choose one or more actions between Start, Stop, Delete, Rename, and Share\.
+ The **Start** action is used to start the head node of a specific cluster\. 
+ The **Stop** action is used to stop the head node of a specific cluster\. A stopped cluster can't serve traffic until it is started again\. 
+ The **Delete** action is used to completely delete all the resources related to the cluster itself\. After a cluster is deleted, it isn't possible to recover it\. A new cluster must be created from the same configuration\. Take extra caution when deleting a cluster, and ensure that data has been appropriately synced prior to deleting a cluster\. 
+ The **Rename** action is used to redefine the label associated with the cluster\. This label is used to refer to the cluster in other EnginFrame views, such as the Service Editor list\. Changing the cluster label doesn't affect the cluster operation or the related AWS CloudFormation stack\. Changing the label automatically updates any service that had previously referred to it as well\. 
+ The **Share** action gives visibility of a cluster to a specific set of user or groups\. By default, only Administrators can see AWS Cloud clusters\. When choosing **Share**, a dialog opens where you can select which users can submit jobs on the cluster\. After choosing **Share**, the previous share settings are overridden\. More specifically, you can choose one of the following options:
  + Only Administrators
  + All Users
  + Selected groups \(here you must select one or more of the groups that you see in the specific area of the dialog\.\)

##### List the existing clusters<a name="list-the-existing-clusters"></a>

1. Log in to the Workspace portal as a user with administrator privileges\.

1. In the menu, select **Switch to Admin View**\.

1. In the navigation pane, under **Infrastructure**, select **Clusters**\.

If the cluster is an AWS ParallelCluster cluster, its type is AWS Cloud\. The allowed actions might vary based on the type and current status of the cluster\.

##### Start a cluster<a name="start-a-cluster"></a>
+ Log in to the Workspace portal as a user with administrator privileges\.
+ In the menu, select **Switch to Admin View**\.
+ In the navigation pane, under **Infrastructure**, select **Clusters**\.
+ Select the **Actions** menu on your chosen configuration\.
+ Choose **Start**\.

  After the **Start** action is selected, users can't see the cluster in their list until the cluster transitions into the **Ready** state\.

##### Stop a cluster<a name="stop-a-cluster"></a>
+ Log in to the Workspace portal as a user with administrator privileges\.
+ In the menu, select **Switch to Admin View**\.
+ In the navigation pane, under **Infrastructure**, select **Clusters**\.
+ Select the **Actions** menu on your chosen configuration\.
+ Choose **Stop**\.

  The cluster isn't available to the users immediately\. After a few moments, it transitions into the **Stopped** state\.

##### Delete a cluster<a name="delete-a-cluster"></a>
+ Log in to the Workspace portal as a user with administrator privileges\.
+ In the menu, select **Switch to Admin View**\.
+ In the navigation pane, under **Infrastructure**, select **Clusters**\.
+ Select the **Actions** menu on your chosen configuration\.
+ Choose **Delete**\.
**Note**  
The cluster must be in a **Stopped** state before it's deleted\.
+ Choose **Yes** on the confirmation dialog\.
+ The selected cluster is deleted after a few minutes, and all its resources are removed\. After this is complete, the cluster transitions into the **Deleted** state\. By default, the entry is removed from the list after one day\.

##### Share a cluster<a name="share-a-cluster"></a>
+ Log in to the Workspace portal as a user with administrator privileges\.
+ In the menu, select **Switch to Admin View**\.
+ In the navigation pane, under **Infrastructure**, select **Clusters**\.
+ Select the **Actions** menu on your chosen configuration\.
+ Choose **Share**\.

  A window opens where you can select users to share the cluster with\.
+ Specify the users to share the cluster with: Only Administrators, All Users, or Selected Groups\.
+ Choose **Save**\.

  When the dialog is closed, the new configuration is applied to the cluster, and it's visible to the specified users or groups depending on its state\.
**Note**  
Only clusters in the **Ready** state are visible to the users\.

##### Rename a cluster<a name="rename-a-cluster"></a>
+ Log in to the Workspace portal as a user with administrator privileges\.
+ In the menu, select **Switch to Admin View**\.
+ In the navigation pane, under **Infrastructure**, select **Clusters**\.
+ Select the **Actions** menu on your chosen configuration\.
+ Choose **Rename**\.
+ Enter a new cluster name in the window\.
+ Choose **Rename**\.
+ The list of clusters is updated after a few moments with the new name chosen for the cluster\.
+ In the **Rename Cluster** box, enter the preferred name in the **Cluster Name** field\.
+ Choose **Rename**\.

##### Current limitations<a name="clusters-view-current-limitations"></a>

HPC Connector supports only jobs that are related to the same cluster in a spooler\.

### Managing jobs<a name="managing-jobs"></a>

To manage a job using HPC Connector, you must specify the cluster where you want to submit a given job\. For this purpose, the service editor allows users to select a cluster by means of the cluster list component\. The component shows the list of clusters that are shared with a given user\.

![\[Select a cluster using the cluster list.\]](http://docs.aws.amazon.com/enginframe/latest/ag/images/jobs-list.png)

On the action script part of your service, the usual `application.submit` action is required to have a `--cluster` option where the selected cluster can be specified\. For HPC Connector to submit jobs remotely, the `--jobmanager` parameter must be set to the `hpc` value\.

A cluster can be specified programmatically using the cluster ID rather than the name\. The cluster ID information is available in the details page of a cluster\. This page is reachable by selecting the name for a given cluster in the clusters page\.

#### Validating a remote job submission<a name="validating-remote-job-submission"></a>

HPC Connector has a mechanism that copies the local data that's required to submit a job remotely\. However, this mechanism is limited to the use of small files, which can't exceed 100MB overall\.

If you run jobs with different requirements in terms of file size, a different approach is required depending on the specific scenario\. AWS provides several solutions for synchronizing data on\-premises remotely\. Solutions such as [AWS DataSync](https://aws.amazon.com/datasync/) or [AWS Storage GateWay](https://aws.amazon.com/storagegateway/?nc=sn&loc=0&whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc), for example, can be used for creating tailor made solutions\. 

Regardless of the synchronization approach adopted, it might happen that the content required on the cloud isn't up to date with the equivalent content on\-premises due to eventual consistency\. In these scenarios, it's useful for a service to fail fast upon a validation check performed before submitting the job to a remote cluster\.

The `HPCC_VALIDATION_SCRIPT_PATH` environment variable allows administrators to specify the path of an executable that is launched before a job is submitted remotely\. The executable has access to all the environment set for the job and therefore can validate if a given job has all the necessary resources for running properly: project files, users, permissions\. 

A validation script is required to return one of two states\.
+ `SUCCESS` indicates that the validation succeeded and that the job is therefore allowed to continue its submission process remotely\.
+ `FAILURE` indicates an issue in the synchronization and cancels the job submission\. A canceled job can then be repeated by the user at a later time\.

Any value that's returned different from `SUCCESS` or `FAILURE` is interpreted by HPC Connector as a failure and HPC Connector cancels the job submission\.

**Note**  
The validation script is meant to perform only a validation of the requirements for job submission\. It's not meant as a way for transferring data from on\-premises\. Due to its scope, it's meant to be run in a short timeframe that's no more than 10 seconds\. Having a validation script that takes near to the 10 second quota to run might cause performance issue in EnginFrame that impacts the whole system\.