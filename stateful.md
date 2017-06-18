### Issue 1:

If persistent disk is created in different gcloud zone than the cluster/node, below error happens for PV creation.

    Error from server (Forbidden): error when creating "https://k8s.io/docs/tasks/run-application/gce-volume.yaml": persistentvolumes "mysql-pv" is forbidden: error querying GCE PD volume mysql-disk: disk is not found
   
Create the persistent disk on same zone.


### Issue 2:

kubectl run -it --rm --image=mysql:5.6 mysql-client -- mysql -h 10.4.1.36 
-ppassword

    10.4.1.36 => describe pods and get pod id
    
    		Name:           mysql-340072548-h1tfz
		Namespace:      default
		Node:           gke-pv-default-pool-a06cab88-k172/10.142.0.2
		Start Time:     Thu, 15 Jun 2017 22:21:47 -0400
		Labels:         app=mysql
		                pod-template-hash=340072548
		Annotations:    kubernetes.io/created-by={"kind":"SerializedReference","apiVersion":"v1","reference":{"kind":"ReplicaSet","nam
		espace":"default","name":"mysql-340072548","uid":"8ae1d41d-523a-11e7-9866-42010a8e0002","a...
		                kubernetes.io/limit-ranger=LimitRanger plugin set: cpu request for container mysql
		Status:         Running
		IP:             10.4.1.36
		Controllers:    ReplicaSet/mysql-340072548
		Containers:
		  mysql:
		    Container ID:       docker://038d520fcdc13e3b8237ec8213a9b14332308ab5105da8255c78c6942258582d
		    Image:              mysql:5.6
		    Image ID:           docker://sha256:ed7b6c642b9dde55c6c86bc58b5d3b571e1a9327c49e32a49433cfe5e792b24d
		    Port:               3306/TCP
		    State:              Running
		      Started:          Thu, 15 Jun 2017 22:21:59 -0400
		    Ready:              True
		    Restart Count:      0
		    Requests:
		      cpu:      100m
		    Environment:
		      MYSQL_ROOT_PASSWORD:      password
		    Mounts:
		      /var/lib/mysql from mysql-persistent-storage (rw)
		      /var/run/secrets/kubernetes.io/serviceaccount from default-token-0j8pc (ro)

### Issue 3:

https://kubernetes.io/docs/tasks/run-application/run-replicated-stateful-application/#deploy-mysql

Remove cpu resource limits at two places for the example to work

