Ansible Docker Deployment Role
==============================

Deployment of a Docker project.

## Requirements

- Docker
- AWS CLI

Role Variables
--------------

- `laravel_deployment_name`: The name that is used to name the directory - most of the times the domain name is used
- `laravel_deployment_release`: The release that is used to name the directory - most of the times its a git tag or timestamp
- `laravel_deployment_archive`: The path to the source files archive (zip) that should be deployed
- `laravel_deployment_number_of_releases`: The number of releases that should be kept

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: krumer.laravel-deployment
          laravel_deployment_name: 'kurmer.it'
          laravel_deployment_release: '1.0.0'
          laravel_deployment_archive: '../../src.zip'
          laravel_deploy_number_of_releases: 15
