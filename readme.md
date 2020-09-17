Ansible Docker Deployment Role
==============================

Deployment of a Docker project.

## Role Variables

- `docker_deployment_project_name`: The name of the project (no whitespaces allowed)
- `docker_deployment_release_name`: The name of the release
- `docker_deployment_release_files`: A list of files that should be copied to the release folder (with local and remote path)
- `docker_deployment_shared_files`: A list of files that should be copied to the shared folder if they don't already exist (with local and remote path)
- `docker_deployment_aws_ecr_repository`: The AWS ECR repository
- `docker_deployment_pre_release_setup_hook`: An optional pre release setup hook, where custom tasks can be executed
- `docker_deployment_post_release_setup_hook`: An optional post release setup hook, where custom tasks can be executed
- `docker_deployment_execution_type`: Defines if the project should be executed as continuously running app or as just a one time running task. (app/task)

## Example Playbook

```yaml
- hosts: all
  roles:
    - role: ansible-docker-deployment
      vars:
        docker_deployment_project_name: project-name
        docker_deployment_release_name: 1
        docker_deployment_release_files:
          - local: docker-compose.run.yml
            remote: docker-compose.yml
          - local: .env
            remote: .env
        docker_deployment_shared_files: []
        docker_deployment_aws_ecr_repository: xxx.dkr.ecr.eu-west-1.amazonaws.com
        docker_deployment_post_release_setup_hook: '{{ playbook_dir }}/hooks/docker_deployment_post_release_setup_hook.yml'
        docker_deployment_execution_type: app
```

## Versioning

In order to have a verioning in place and working, create leightweight tags that point to the appropriate minor release versions.

Creating a new minor release:

```bash
git tag 1.0
git push --tags
```

Replacing an already existing minor release:

```bash
git tag -d 1.0
git push origin :refs/tags/1.0
git tag 1.0
git push --tags
```
