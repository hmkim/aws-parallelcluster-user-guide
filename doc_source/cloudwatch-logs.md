# Integration with Amazon CloudWatch Logs<a name="cloudwatch-logs"></a>

Starting with AWS ParallelCluster version 2\.6\.0, common logs are stored in CloudWatch Logs by default\. For more information about CloudWatch Logs, see [Amazon CloudWatch Logs User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/)\. To configure CloudWatch Logs integration, see the [`[cw_log]` section](cw-log-section.md) and the [`cw_log_settings`](cluster-definition.md#cw-log-settings) setting\.

A log group is created for each cluster with a name `/aws/parallelcluster/cluster-name` \(for example, `/aws/parallelcluster/testCluster`\)\. Each log \(or set of logs if the path contains a `*`\) on each node has a log stream named `{hostname}.{instance_id}.{logIdentifier}`\. \(For example `ip-172-31-10-46.i-02587cf29cc3048f3.nodewatcher`\.\) Log data is sent to CloudWatch by the [CloudWatch agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html), which runs as `root` on all cluster instances\.

Starting with AWS ParallelCluster version 2\.10\.0, an Amazon CloudWatch dashboard is created when the cluster is created\. This dashboard makes it easy to review the logs stored in CloudWatch Logs\. For more information, see [Amazon CloudWatch dashboard](cloudwatch-dashboard.md)\.

This list contains the path of the logs and the *logIdentifier* used for those logs\.
+ `/opt/sge/default/spool/qmaster/messages` \(`sge-qmaster`\)
+ `/var/log/cfn-init.log` \(`cfn-init`\)
+ `/var/log/chef-client.log` \(`chef-client`\)
+ `/var/log/cloud-init.log` \(`cloud-init`\)
+ `/var/log/cloud-init-output.log` \(`cloud-init-output`\)
+ `/var/log/dcv/agent.*.log` \(`dcv-agent`\)
+ `/var/log/dcv/dcv-xsession.*.log` \(`dcv-xsession`\)
+ `/var/log/dcv/server.log` \(`dcv-server`\)
+ `/var/log/dcv/sessionlauncher.log` \(`dcv-session-launcher`\)
+ `/var/log/dcv/Xdcv.*.log` \(`Xdcv`\)
+ `/var/log/jobwatcher` \(`jobwatcher`\)
+ `/var/log/messages` \(`system-messages`\)
+ `/var/log/nodewatcher` \(`nodewatcher`\)
+ `/var/log/parallelcluster/clustermgtd` \(`clustermgtd`\)
+ `/var/log/parallelcluster/computemgtd` \(`computemgtd`\)
+ `/var/log/parallelcluster/pcluster_dcv_authenticator.log` \(`dcv-authenticator`\)
+ `/var/log/parallelcluster/pcluster_dcv_connect.log` \(`dcv-ext-authenticator`\)
+ `/var/log/parallelcluster/slurm_resume.log` \(`slurm_resume`\)
+ `/var/log/parallelcluster/slurm_suspend.log` \(`slurm_suspend`\)
+ `/var/log/slurmctld.log` \(`slurmctld`\)
+ `/var/log/slurmd.log` \(`slurmd`\)
+ `/var/log/sqswatcher` \(`sqswatcher`\)
+ `/var/log/supervisord.log` \(`supervisord`\)
+ `/var/log/syslog` \(`syslog`\)
+ 
**Note**  
Starting with version 2\.11\.5, AWS ParallelCluster doesn't support the use of SGE or Torque schedulers\.

  `/var/spool/sge/*/messages` \(`sge-exec-daemon`\)
+ `/var/spool/torque/client_logs/*` \(`torque-client`\)
+ `/var/spool/torque/server_logs/*` \(`torque-server`\)

Jobs in clusters that use AWS Batch store the output of jobs that reached a `RUNNING`, `SUCCEEDED`, or `FAILED` state in CloudWatch Logs\. The log group is `/aws/batch/job`, and the log stream name format is `jobDefinitionName/default/ecs_task_id`\. By default, these logs are set to never expire, but you can modify the retention period\. For more information, see [Change log data retention in CloudWatch Logs](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/SettingLogRetention.html) in the *Amazon CloudWatch Logs User Guide*\.

**Note**  
`chef-client`, `cloud-init-output`, `clustermgtd`, `computemgtd`, `slurm_resume`, and `slurm_suspend` were added in AWS ParallelCluster version 2\.9\.0\. For AWS ParallelCluster version 2\.6\.0, `/var/log/cfn-init-cmd.log` \(`cfn-init-cmd`\) and `/var/log/cfn-wire.log` \(`cfn-wire`\) were also stored in CloudWatch Logs\.