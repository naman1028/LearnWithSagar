# Day 4 - Practice Questions


```
1. Create a new file Dockerfile to build a container image from. It should:
    use bash as base
    run ping google.com
    Build the image and tag it as pinger.
    Run the image (create a container) named my-ping.
#vi Dockerfile
  FROM bash
  CMD  ["ping","google.com"]
:wq
#docker build -t pinger .
#docker run --name=my-ping -it pinger
2. Tag the image, which is currently tagged as pinger , also as local-registry:5000/pinger .
#docker tag pinger local-registry:5000/pinger

3. Create a namespace called 'mynamespace' and a pod with image nginx in mynamespace
#kubectl create ns mynamespace
#kubectl run nginx --image=nginx -n mynamespace

4. Create a busybox pod (using YAML) that runs the command "env".
# kubectl run busybox --image=busybox  -it --restart=Never -- /bin/sh -c 'env'

5. Get the YAML for a new namespace called 'myns' without creating it
#kubectl create ns myns --dry-run=client  -o yaml > myns.yaml

6. Get pods on all namespaces
#k get pods -A

7. Get information about the pod, including details about potential issues (e.g. pod hasn't started)
# k log podname
#k describe pod podname

8. Create a busybox pod that echoes 'hello world' and then exits
# k run busybox2 --image=busybox  --rm -it --restart=Never -- echo 'hello world'

9. Delete the pod you just created without any delay (force delete)
#k delete pod podname --grace-period=0 --force

10. Create the nginx pod with version 1.17.4 and expose it on port 80
  # k run pod2  --image=nginx:1.17.4
  # k expose pod pod2 --port 80   
11. Change the Image version to 1.15-alpine for the pod you just created and verify the image version is updated
# k set image pod/pod2  pod2=alpine:1.15
# k describe pod pod2 | grep -w 'Image:'
12. Change the Image version back to 1.17.1 for the pod you just updated and observe the changes
#k set image pod/pod2  pod2=nginx:1.17.4
13. Create a Pod with three busy box containers with commands “ls; sleep 3600;”, “echo Hello World; sleep 3600;” and “echo this is the third container; sleep 3600” respectively and check the status
# vi bbox.yaml
apiVersion: v1
kind: Pod
metadata:
    labels:
      run: bbox
    name: bbox
spec:
  containers:
  - image: busybox
    name: bbox1
    command: ["/bin/sh","-c","ls; sleep 3600;"]
  - image: busybox
    name: bbox2
    command: ["/bin/sh","-c","echo Hello World; sleep 3600;"]
  - image: busybox
    name: bbox3
    command: ["/bin/sh","-c","echo this is the third container; sleep 3600"]
:wq
# k create -f bbox.yaml
# k get pods

14. Show metrics of the above pod containers and puts them into the file.log and verify
# k top pod bbox --containers=true  > file.log
# cat file.log

15. Create a Docker file and save the file in directory /opt/ldh/Question12
    The Docker file run an alpine image with the command "echo hello linuxdatahub" as the default command. 
    Build the image, and export it in OCI format to a file file with the name "linuxdocker" and tag should be 9.8. 
    Use sudo wherever required.
# cd  /opt/ldh/Question12
# vi Dockerfile
FROM alpine
CMD echo hello linuxdatahub
:wq
#docker buildx build -o type=oci,dest=linuxdocker -f Dockerfile .  (Not sure if this is right )
OR
# docker build -t linuxdocker:9.8 .
# docker export linuxdocker:9.8 > linuxdocker 


16. Create a container from the attached Dockerfile and index.html.
    Name the image my-image.
    Run the container exposing port 8080 on the host and port 80 on the container.
    Name the container my-container. 
    Stop the container. 
    Delete the container.
    Save image in tar file format.

#docker build -t my-image .
#docker run  --name=my-container -p 8080:80 my-image
#docker stop my-container
#docker rm my-container
#docker save my-image > my-image.tar



```
