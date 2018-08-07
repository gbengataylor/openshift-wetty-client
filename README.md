# OpenShift wetty client
Containerized OpenShift CLI tools accessible via wetty

## What is this?
This provides a web console to a pod with the oc CLI tool available. That's it. 

Need oc but don't have a terminal or the ability to install anything? Just run this as a pod in your project - or run it to share for a whole team.

## How do I use this?
You need to be a cluster admin or have your cluster admin relax the SCC restrictions in your cluster so that this image is allow to run as root. The command for that is:
    `oc adm policy add-scc-to-group anyuid system:authenticated`

Now you can
* Create a project in openshift : `oc new-project occli`
* Deploy the prebuilt image : `oc new-app quay.io/jasonredhat/openshift-wetty-client`
* Expose a route on port 8888 : `oc expose svc/openshift-wetty-client --port 8888` 

Navigate to the exposed route and login as one of the 20 available users (term1-term20). There are 20 users created in the Dockerfile with username matching the password.

Now in that wetty terminal login to your OpenShift cluster of choice using the oc command:
>`oc login https://mycluster.awesomeland.com`

and run whatever commands you want:
>`oc get pods --all-namespaces`

## WARNING
 - THIS CONTAINER CURRENTLY REQUIRES BEING RUN AS ROOT

That is root inside the container not of the platform. But it adds an extra layer of security risk. So bewarned...

## TODOs
* Fix this image so that it can run as any random numerical UID and not as root
* Create the users list from a config files (name/password)
