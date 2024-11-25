# Gitops Pipelines

## Gitops Repository Pull-Request Checker 
 
This pipeline is used to validate pull-requests into the gitops repository. This runner will call the gitops-pull-request pipeline which will validate the images being updated. Its' designed to be used for promotion flows, where the state of one environment is being promoted to the successor environment (dev to stage, or stage to prod).

Tasks references come from this repository ` ../pipelines` `../tasks` and are referenced by URL using the git resolver in tekton. 
 
When the pipleines in this repo are updated, all future runs in existing pipelines are shared.

A developer can override these tasks with a local copy and updated annotations. 

Example 

To override the git-clone task, you may simply copy the git reference into your .tekton directory and then reference it from the remote task annotation. 

`pipelinesascode.tekton.dev/task-0: ".tekton/git-clone.yaml"` 
   

## Templates 
These pipelines are in template format. The references to this repository in the PaC template is `{{values.rawUrl}}` which is updated to point to this repo or the fork of this repo.

The intent of the template is to be able to fork this repository and update its use in the Developer Hub templates directory. 

Elevate your development with secure templates
If you have the Red Hat Trusted Application Pipeline (RHTAP) installed, Red Hat Developer Hub becomes even more powerful. RHTAP provides additional secure software templates that you can use right within RHDH. These templates help you integrate advanced security measures into your development process seamlessly, without adding complexity. 

By integrating Red Hat Trusted Artifact Signer (RHTAS) for code integrity, Red hat Trusted Profile Analyzer (RHTPA) for automated SBOM creation, and Red Hat Advanced Cluster Security (RHACS) for proactive vulnerability scanning, RHTAP strengthens your security posture with advanced tools, offering a robust defense against security threats throughout the development lifecycle.
Ready-to-use secure templates: Jumpstart your projects with templates that incorporate industry-leading security practices. RHTAP ensures that every line of code contributes to a fortress of security significantly enhancing early vulnerability detection and mitigation.
Seamless integration:  The secure templates from RHTAP slide right into your existing workflows, so there’s no extra work for your team. By aligning with Supply-chain Levels for Software Artifacts (SLSA) Level 3 RHTAP’s pioneering secure CI/CD framework upholds the highest standards in software development.
Focus on innovation: With security built into your templates, RHTAP helps you adopt a DevSecOps culture. This allows your developers to concentrate on building great features without getting bogged down by security setups.

I would add on a sentence or two to this section to highlight that RHTAP includes DH, TAS, TPA, Quay, and ACS to make the feature highlights per product more clear that they are connected with RHTAP. Also, by highlighting that RHTAP includes DH and more-you are getting the security features that come with those other products.

