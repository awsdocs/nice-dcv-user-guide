# Linux Client<a name="client-linux"></a>

The Linux client runs natively on the operating system and let you to connect to NICE DCV sessions hosted on Windows and Linux NICE DCV servers\.

The Linux client is installed on a Linux client computer using a software package\. The software package installs all required packages and their dependencies, and performs the required client configuration\.

For more information about connecting to a NICE DCV session using the Linux client, see [Connecting to a NICE DCV Session Using the Linux Client](using-connecting-linux.md)\.

**To install the Linux client**

1. The software packages are digitally signed with a secure GPG signature\. To allow the package manager to verify the package signature, you must import the NICE GPG key\. Open a terminal window and import the NICE GPG key\.
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

1. Download the appropriate client software package for your operating system\.
   + RHEL 7\.x and CentOS 7\.x

     ```
     $  wget https://d1uj6qtbmh3dt5.cloudfront.net/2021.0/Clients/nice-dcv-viewer-2021.0.3294-1.el7.x86_64.rpm
     ```
   + RHEL 8\.x and CentOS 8\.x

     ```
     $  wget https://d1uj6qtbmh3dt5.cloudfront.net/2021.0/Clients/nice-dcv-viewer-2021.0.3294-1.el8.x86_64.rpm
     ```
   + Ubuntu 16\.04

     ```
     $  wget https://d1uj6qtbmh3dt5.cloudfront.net/2021.0/Clients/nice-dcv-viewer_2021.0.3294-1_amd64.ubuntu1604.deb
     ```
   + Ubuntu 18\.04

     ```
     $  wget https://d1uj6qtbmh3dt5.cloudfront.net/2021.0/Clients/nice-dcv-viewer_2021.0.3294-1_amd64.ubuntu1804.deb
     ```
   + Ubuntu 20\.04

     ```
     $  wget https://d1uj6qtbmh3dt5.cloudfront.net/2021.0/Clients/nice-dcv-viewer_2021.0.3294-1_amd64.ubuntu2004.deb
     ```
   + SUSE Linux Enterprise 15

     ```
     $  curl-O https://d1uj6qtbmh3dt5.cloudfront.net/2021.0/Clients/nice-dcv-viewer-2021.0.3294-1.sles15.x86_64.rpm
     ```

1. Install the Linux client\.
   + RHEL 7\.x and CentOS 7\.x

     ```
     $  sudo yum install nice-dcv-viewer-2021.0.3294-1.el7.x86_64.rpm
     ```
   + RHEL 8\.x and CentOS 8\.x

     ```
     $  sudo yum install nice-dcv-viewer-2021.0.3294-1.el8.x86_64.rpm
     ```
   + Ubuntu 16\.04

     ```
     $  sudo dpkg --install nice-dcv-viewer_2021.0.3294-1_amd64.ubuntu1604.deb
     ```
   + Ubuntu 18\.04

     ```
     $  sudo dpkg --install nice-dcv-viewer_2021.0.3294-1_amd64.ubuntu1804.deb
     ```
   + Ubuntu 20\.04

     ```
     $  sudo dpkg --install nice-dcv-viewer_2021.0.3294-1_amd64.ubuntu2004.deb
     ```
   + SUSE Linux Enterprise 15

     ```
     $  sudo zypper install nice-dcv-viewer-2021.0.3294-1.sles15.x86_64.rpm
     ```