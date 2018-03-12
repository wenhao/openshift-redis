# openshift-redis
OpenShift Redis Cluster


# Create a bootstrap master
oc create -f redis-master-pod.yaml

# Create a service to track the sentinels
oc create -f redis-sentinel-service.yaml

# Create a replication controller for redis servers
oc create -f redis-slave-controller.yaml

# Create a replication controller for redis sentinels
oc create -f redis-sentinel-controller.yaml

# Scale both replication controllers
oc scale rc redis --replicas=3
oc scale rc redis-sentinel --replicas=3

# Delete the original master pod
# Note: If you are running all the above commands consecutively including this one in a shell script, it may NOT work out. When you run the above commands, let the pods first come up, especially the redis-master pod. Else, the sentinel pods would never be able to know the master redis server and establish a connection with it.
oc delete pods redis-master
