### Issue 1:

If persistent disk is created in different gcloud zone than the cluster/node, below error happens for PV creation.

    Error from server (Forbidden): error when creating "https://k8s.io/docs/tasks/run-application/gce-volume.yaml": persistentvolumes "mysql-pv" is forbidden: error querying GCE PD volume mysql-disk: disk is not found
   
Create the persistent disk on same zone.
