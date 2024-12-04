include:
 - project: 'paas/gitlab-cicd-templates'
   ref: 1.0.0
   file: '/python-validate.yml'
 - project: 'paas/gitlab-cicd-templates'
   ref: 1.0.0
   file: '/buildah.yml'
 - project: 'paas/gitlab-cicd-templates'
   ref: 1.0.0
   file: '/image-scan.yml'
 - project: 'paas/gitlab-cicd-templates'
   ref: 1.0.0
   file: 'sonarqube.yml'

validate:lint:
  tags:
    - openshift
  variables:
    KUBERNETES_MEMORY_LIMIT: "6Gi"
  extends:
    - .python-validate:lint
  allow_failure: true

validate:security:
  tags:
    - openshift
  variables:
    KUBERNETES_MEMORY_LIMIT: "6Gi"
  extends:
     - .python-validate:security
  allow_failure: true

validate:sonarqube:
  tags:
    - openshift
  stage: validate
  extends:
     - .sonarqube
  allow_failure: true

build:
  tags:
    - openshift
  variables:
    OCI_IMAGE_NAME: images.paas.redhat.com/opl-ui/opl-ui-app
  extends:
    - .buildah:build
  artifacts:
    paths:
      - tenant-operator.tar

image-scan:
  tags:
    - openshift
  extends:
    - .image-scan
  allow_failure: true

image-push:
  tags:
    - openshift
  variables:
    OCI_IMAGE_NAME: images.paas.redhat.com/opl-ui/opl-ui-app
  extends:
    - .buildah:image-push

stages:
  - validate
  - test
  - build
  - image-scan
  - image-push
