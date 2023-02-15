# Using the Log Files<a name="troubleshooting-logs"></a>

Use the NICE DCV client log files to identify and troubleshoot problems with your NICE DCV client\. Logs aren't enabled by default on Windows clients\. After logs are enabled, the log files are stored in the following location on your NICE DCV client:
+ Windows client

  ```
  C:\ProgramData\client.log
  ```
**Note**  
By default, the `ProgramData` folder might be hidden\. If you don't see the `ProgramData` folder, set your file browser to show hidden items\. Alternatively, enter `%programdata%` in the address bar and press **Enter**\.
+ Linux or macOS client

  ```
  ~/.local/share/NICE/dcvviewer/log/viewer.log
  ```

**To enable NICE DCV to store log files on a Windows client**

1. Navigate to the folder where the `dcvviewer.exe` file is located\. \(By default, this is `C:\Program Files (x86)\NICE\DCV\Client\bin\`\.\) Then, open a command prompt window\.

1. Launch NICE DCV client using the command line interface\.

   ```
   dcvviewer --log-level info --log-file-name C:/ProgramData/client.log
   ```

   Or add the following configuration to the [connection file](using-connection-file.md):

   ```
   [debug]
   logfilename=C:/ProgramData/client.log
   loglevel=info
   ```