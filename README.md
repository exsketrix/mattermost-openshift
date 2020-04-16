# mattermost-openshift

This repository contains an Ansible role that provides a means for deploying Mattermost to Openshift.

## Requirements

Requirements to run this Ansible role:

* Docker installed
* Ansible v2.6+
* An account on OpenShift with at least deployer access to a project/namespace
* The 'exsketrix/openshift-app-deployer.git' Ansible role should be installed alongside this role.

## Variables

This role performs validation to check that all mandatory variables are populated. The following table lists each variable that can be set for this role:

| Variable Name                                   |  Required | Example Value                                              |
| ----------------------------------------------- | --------- | ---------------------------------------------------------- |
| mattermost_openshift_postgres_password          | Y         | <postgres_password> - must be base64 encoded               |
| mattermost_openshift_internal_tag               | Y         | prod-latest                                                |
| mattermost_openshift_docker_registry_host       | Y         | nexus.bizchat.io                                           |
| mattermost_openshift_docker_registry_port       | Y         | 18999                                                      |
| mattermost_openshift_app_version_tag            | Y         | 5.21.0                                                     |
| mattermost_openshift_nginx_version_tag          | Y         | 1.17.9                                                     |

This role also requires all the mandatory variables of the openshift-app-deployer role to be populated. The following variables required in the openshift-app-deployer role have been given default values in this role which can be overriden if required:

* openshift_app_deployer_resources
* openshift_app_deployer_files_resource_path
* openshift_app_deployer_templates_resource_path 

## Installation into Ansible Playbook

Create/Edit requirements yml file in playbook, adding the following dependency:

```yaml
- src: git@github.com:exsketrix/mattermost-openshift.git
  scm: git
  version: master
  name: mattermost-openshift
- src: git@github.com:exsketrix/openshift-app-deployer.git
  scm: git
  version: master
  name: openshift-app-deployer
```
