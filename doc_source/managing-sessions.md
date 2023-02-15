# Managing the sessions directory<a name="managing-sessions"></a>

This chapter illustrates the basic concepts that concern EnginFrame interactive session data and its management\. 

The data of an interactive session is in a dedicated data container\. This container is created by EnginFrame to host the files that are required for the interactive session lifecycle\. These include the thumbnail of a screenshot, for example\. 

`INTERACTIVE_SHARED_ROOT` is organized in the same way as the EnginFrame spoolers\. For more information, see [Managing spoolers](managing-spoolers.md)\. Under `INTERACTIVE_SHARED_ROOT`, EnginFrame creates a directory for each user the first time an interactive session is created\. These directories are named with the user's names\. Under each `<username>` directory, EnginFrame creates its session data directory, one for each interactive session\. 

## Sessions requirements<a name="sessions-directory-requirements"></a>

Sessions must reside on a *shared file system* that must be mounted from the EnginFrame Server's host, EnginFrame Agent's host and visualization nodes\. This area might not require to be shared when submitting sessions to some Distributed Resource Managers\. For more information, see [Shared file system requirements](planning-deployment.md#interactive-shared-file-system-requirements)\. 

The `INTERACTIVE_SHARED_ROOT` directory must be owned by the user that's running EnginFrame Server \(for example, `efnobody`\) and by `efnobody`'s primary group\. It must have the `3777` permissions\. To summarize, the following permissions are required: `d rwx rws rwt efnobody:efnogroup` where `efnogroup` is `efnobody`'s primary group\.

The EnginFrame installer creates this directory with the proper permissions on your behalf\. The default location is `$EF_TOP/sessions`\. You can change the `INTERACTIVE_SHARED_ROOT` value in the `$EF_TOP/conf/plugins/interactive/interactive.efconf` file\. 

This shared area has to be readable and writable by EnginFrame nodes and visualization nodes\. EnginFrame provides a mapping mechanism that enables these file\-systems to be mounted with different paths on EnginFrame and visualization hosts\. This configuration is specific to the Distributed Resource Manager that's used for the session and can be configured in the specific plugin configuration file:
+  On PBS Professional®, use `PBS_INTERACTIVE_SHARED_ROOT_EXEC_HOST` in the `$EF_TOP/conf/plugins/pbs/ef.pbs.conf` file\.
+  On SLURM™, use `SLURM_INTERACTIVE_SHARED_ROOT_EXEC_HOST` in the `$EF_TOP/conf/plugins/slurm/ef.slurm.conf` file\.
+  On SGE, use `SGE_INTERACTIVE_SHARED_ROOT_EXEC_HOST` in the `$EF_TOP/conf/plugins/sge/ef.sge.conf` file\. 