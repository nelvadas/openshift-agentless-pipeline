# openshift-agentless-pipeline

An agentless pipeline build relying on an S2I image.
The build runs in jenkins (agent none) and creates if required the sub-build using s2i.
Then the build is monitored and when finished, it tags and deploy the app.

```
# oc create secret generic my-secret --from-literal=username=user \
#                                    --from-literal=password=password

oc create secret generic git-repo-secret --from-file=ssh-privatekey=~/.ssh/id_rsa
GIT_REPO=https://github.com/akram/penshift-agentless-pipeline.git
oc new-build --name=my-pipeline --strategy=pipeline \
             --source=$GIT_REPO
oc env bc my-pipeline GIT_SSL_NO_VERIFY=true
```
