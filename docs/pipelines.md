Login to image registry
Podman login registry.redhat.io - u rarnaud@redhat.com
Password


Download the image
Podman pull registry.redhat.io/rhtap-cli/rhtap-cli-rhel9:latest

Open the shell in the container than is using that image

Podman run -it –entrypoint bash –env-file tmp/private.env –publish 8228:8228 –rm rhtap-cli <image that you downlioaded abova>

Here bash is used so that we can have that shell
Using an env file so that we do not have to disclose my credentials
Publish to port to 8228 because we have a web service that’s going to interact with GitHub to create a GitHub application when we’re going to run the github app integration command in the later processes.


Login to your cluster <command>
Create a config file
rhtap-cli config - - create


This file contains a big chunk of configuration about how RHTAP is deployed.

Browse back to the  cluster UI. 
In the Administrator view, select Workdloads < ConfigMaps
Select RHTAP project, select rhtap-cli-config
Select YAML view and navigate to where config.yaml parameters are defined.



Namespace, is the default namespace where the  RHTAP config will be stored.
Then we have a feature section that controls all the products that will be deployed by the installer.

ACS - disabled that is false

Quay - disabled that is false

catalogURL - update it to your fork instance URL

manageSubscrioption property is all there in the file, it is there because if the platform engineer deploys RHTAP in a cluster that already has some of the required subscriptions, this file will ensure to use the exiting ones and the install process will not fail.

Select the save button.

Come back to the terminal again

I want to deall with the external services that I want to integrate with my deployment
GitHub integration


chtap-cli integration github0-app \
–create \
–token=”$GITHJUB__ORG_TOKEN” \
–prg=”GITHUB__ORG” \
“rhtap-$GITHUb__ORG-demo”

All these integrations



Data is coming from the private.env file

Come back to the cluster UI
In the Administrator view > expand Workloads and then select Secrets, you can see all the integrations
These secrets will be read by the HELM chart to integrate the services during deployment.

Deploy RHTAP
Rhtap-cli deploy

