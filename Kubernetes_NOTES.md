Kubernetes Objects

  Pod
  Service
  Volume
  Namespace

In addition, Kubernetes contains a number of higher-level abstractions called Controllers.
They include:

    ReplicaSet
    Deployment
    StatefulSet
    DaemonSet
    Job





Required Fields

In the .yaml file for the Kubernetes object you want to create,
you’ll need to set values for the following fields:

  apiVersion - Which version of the Kubernetes API you’re using to create this object
  kind - What kind of object you want to create
  metadata - Data that helps uniquely identify the object, including a name string, UID, and optional namespace
  *spec - The precise format of the object spec is different for every Kubernetes object, and contains nested fields specific to that object

POD object sample:
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: busybox
    command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']
