# Collaborating on a NICE DCV session<a name="managing-sessions-session-collaboration"></a>

NICE DCV users can collaborate on the same session, enabling screen and mouse sharing\. Users can join authorized sessions while session owners can disconnect users from any session collaboration\. To take advantage of this feature, users must be joining the same session identified by the same session ID\.

**Requirements**

By default, the only user that can connect to a DCV session is the owner of that session\.

For users to collaborate on the same session, the active permissions applied to the session need to be updated to include the `display` parameter\. For more information on editing the permissions file, see [ Configuring NICE DCV authorization](https://docs.aws.amazon.com/dcv/latest/adminguide/security-authorization.html)\.

**Note**  
Administrator privileges are required to edit the permissions file\.

**To collaborate on NICE DCV sessions for Windows or Linux based servers:**

1. Choose the **Collaborators** icon on the NICE DCV client located in the DCV toolbar\.  
![\[Collaborators icon on the DCV client\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/collaboration.png)

   A **Collaborators Window** will open showing all of the connected NICE DCV sessions available\.

1. Select a session to join\.

1. Choose **Disconnect**, to remove all client connections, except yours, from the DCV session\.

   This option is only available for session owners\.  
![\[Collaborating user sessions\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/collaboration-users.png)

1. Choose **Disconnect** to remove an user from an active session\.

**To collaborate on NICE DCV sessions for macOS:**

1. Go to **View** on the top toolbar\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/MACDropDown.png)

1. Choose **Collaborators** from the drop\-down menu\.

   A **Collaborators Window** will open showing all of the connected NICE DCV sessions available\.  
![\[Collaborating user sessions\]](http://docs.aws.amazon.com/dcv/latest/userguide/images/collaboration-users.png)

1. Select the session to join\.

1. Choose **Disconnect** to remove all client connections except yours from the DCV session\.

   This option is only available for session owners\.