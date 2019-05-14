# Linux Client<a name="client-linux"></a>

NICE DCV offers client applications that run on the following Linux operating systems:
+ RHEL 7\.x and CentOS 7\.x
+ SUSE Linux Enterprise 12\.x
+ Ubuntu 16\.04 and 18\.04

The applications run natively on the operating system and enable you to connect to NICE DCV sessions hosted on Windows and Linux NICE DCV servers\.

**Topics**
+ [Requirements](#client-lin-requirements)
+ [Limitations](#client-linux-limitations)
+ [Installing the Linux Client](#client-linux-install)

## Requirements<a name="client-lin-requirements"></a>

The Linux client must be able to connect to the NICE DCV server\. It must also be able to communicate over the required port \(8443 by default\)\.

## Limitations<a name="client-linux-limitations"></a>

The Linux client has the following limitations:
+ It does not support USB remotization\.
+ It does not support audio\.

## Installing the Linux Client<a name="client-linux-install"></a>

To use the Linux client on your computer, you must first install it\.

The Linux client is installed on a Linux client computer using a software package\. The software package installs all required packages and their dependencies, and performs the necessary client configuration\.

**To install the Linux client**

1. The software packages are digitally signed with a secure GPG signature\. To allow the package manager to verify the package signature, you must import the NICE GPG key\. Open a terminal window and import the NICE GPG key\.
   + RHEL 7\.x, CentOS 7\.x, and SUSE Linux Enterprise 12\.x

     ```
     $ sudo rpm --import https://s3-eu-west-1.amazonaws.com/nice-dcv-publish/NICE-GPG-KEY
     ```
   + Ubuntu

     Download the GPG key\.

     ```
     $ wget https://s3-eu-west-1.amazonaws.com/nice-dcv-publish/NICE-GPG-KEY
     ```

     Install the GPG key\.

     ```
     $ sudo apt-key add NICE-GPG-KEY
     ```

1. Download the appropriate client software package for your operating system\.
   + RHEL 7\.x and CentOS 7\.x

     ```
     $  wget https://d1uj6qtbmh3dt5.cloudfront.net/client/nice-dcv-viewer-2017.4.version.el7.x86_64.rpm
     ```
   + SUSE Linux Enterprise 12\.x

     ```
     $  wget https://d1uj6qtbmh3dt5.cloudfront.net/client/nice-dcv-viewer-2017.4.version.sles12.x86_64.rpm
     ```
   + Ubuntu 16\.04

     ```
     $  wget https://d1uj6qtbmh3dt5.cloudfront.net/client/nice-dcv-viewer_2017.4.version_amd64.ubuntu1604.deb
     ```
   + Ubuntu 18\.04

     ```
     $  wget https://d1uj6qtbmh3dt5.cloudfront.net/client/nice-dcv-viewer_2017.4.version_amd64.ubuntu1804.deb
     ```

1. Install the Linux client\.
   + RHEL 7\.x and CentOS 7\.x

     ```
     $  sudo yum install nice-dcv-viewer-2017.4.version.el7.x86_64.rpm
     ```
   + SUSE Linux Enterprise 12\.x

     ```
     $  sudo zypper install nice-dcv-viewer-2017.4.version.sles12.x86_64.rpm
     ```
   + Ubuntu 16\.04

     ```
     $  sudo dpkg --install nice-dcv-viewer_2017.4.version_amd64.ubuntu1604.deb
     ```
   + Ubuntu 18\.04

     ```
     $  sudo dpkg --install nice-dcv-viewer_2017.4.version_amd64.ubuntu1804.deb
     ```