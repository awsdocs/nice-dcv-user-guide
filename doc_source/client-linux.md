# Linux client<a name="client-linux"></a>

The Linux client runs natively on the operating system\. You can use it to connect to NICE DCV sessions that are hosted on Windows and Linux NICE DCV servers\.

You install the Linux client on a Linux client computer using a software package\. The software package installs all required packages and their dependencies, and performs the required client configuration\.

For instructions on how to connect to a NICE DCV session using the Linux client, see [Connecting to a NICE DCV session using the Linux client](using-connecting-linux.md)\.

**To install the Linux client**

1. The software packages are digitally signed with a secure GPG signature\. To allow the package manager to verify the package signature, import the NICE GPG key\. To do this, open a terminal window and import the NICE GPG key\.
   + RHEL 7\.x/8\.x, CentOS 7\.x/8\.x, and SUSE Linux Enterprise 15

     ```
     $ sudo rpm --import https://d1uj6qtbmh3dt5.cloudfront.net/NICE-GPG-KEY
     ```
   + Ubuntu

     Download the GPG key\.

     ```
     $ wget https://d1uj6qtbmh3dt5.cloudfront.net/NICE-GPG-KEY
     ```

     Install the GPG key\.

     ```
     $ sudo apt-key add NICE-GPG-KEY
     ```

1. Download the appropriate client software package for your target operating system from the [NICE DCV](http://download.nice-dcv.com) website\.
**Tip**  
The [latest packages](http://download.nice-dcv.com/latest.html) page of the download website contains links that always point to the newest available version\. You can use these links to automatically retrieve the newest NICE DCV packages\.

1. Install the Linux client\. Enter the filename of the downloaded file to complete the following command\.
   + RHEL 7\.x and CentOS 7\.x

     ```
     $  sudo yum install the downloaded .rpm file
     ```
   + RHEL 8\.x and CentOS 8\.x

     ```
     $  sudo yum install the downloaded .rpm file
     ```
   + Ubuntu 18\.04

     ```
     $  sudo dpkg --install the downloaded .deb file
     ```
   + Ubuntu 20\.04

     ```
     $  sudo dpkg --install the downloaded .deb file
     ```
   + SUSE Linux Enterprise 15

     ```
     $  sudo zypper install the downloaded .rpm file
     ```