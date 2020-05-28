# Git Cheat Sheets


## GitLab

### Gitlab CI-CD

### Reference

Pay attention that the correct file for gitlab ci-cd pipeline `.gitlab-ci.yml` ends with `.yml`, not `.yaml`.

### Choose which executor for gitlab runner

### Increase concurrent jobs

Jobs are executed by Runners. Multiple jobs in the same stage are executed in parallel, if there are enough concurrent runners.

The limit of concurrent jobs are tunable in [config.toml](https://docs.gitlab.com/runner/configuration/advanced-configuration.html).

### Job image vs docker executor

In the definition of jobs, the `image` keyword is the name of the Docker image the **Docker executor** will run to perform the CI tasks.

> Check if other executors like ssh can consume the `image` keyword

### Services in jobs

The `services` keyword defines just another Docker image that is run during your job and is linked to the Docker image that the image keyword defines. This allows you to access the service image during build time. This feature is designed to provide network accessible services. A database is the simplest example of such a service. [Do not use services as tools for the jobs](https://docs.gitlab.com/ee/ci/docker/using_docker_images.html#what-services-are-not-for).

### Semantic versioning

[Semantic release](https://github.com/semantic-release/semantic-release) allows automatic versioning and package publishing. How does it work?

- Follow [Angular commit message convention](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines) during development phase
- Host code in a git repository
- Create a working CI pipeline, i.e. add a working .gitlab-ci.yml file to project
- Install git 2.7.1 minimum, node.js 10.18 minimum and semantic-release in CI environment. These tools can be installed in a job of Jenkins runner, or be ready with a Jenkins runner based of node.js image
- Configure CI service to expose the access token in the environment variable and run semantic-release during the versioning job
- Add configuration file
  - include branches
  - include plugins (depending on CI environment)
- Trigger the CI pipeline

### Debugging in gitlab runners

- Run gitlab-runner in [debug mode](https://docs.gitlab.com/runner/faq/#run-in---debug-mode):

  ```bash
  gitlab-runner --debug run
  ```

- [Use Interactive Web Terminals](https://docs.gitlab.com/ee/ci/interactive_web_terminal/)
  - Support for Docker executor is [underway](https://gitlab.com/gitlab-org/gitlab-runner/issues/3605)

- Gitlab has numerous [built-in environment variables](https://docs.gitlab.com/ee/ci/variables/predefined_variables.html) for the pipeline runtime. Take advantage of them.

### Troubleshooting

Nested reference of variables is not working in `gitlab-ci.yml`.

```bash
$ cat .gitlab-ci.yml

variables:
  PROJECT_NAME: $CI_PROJECT_NAME # default CI variable of gitlab

job-sample:
  stage: stage-sample
  image: docker
  variables:
    BUILD_PROJECT_NAME: $PROJECT_NAME # Don't. $CI_PROJECT_NAME will not be evaluated here
  services:
    - docker:dind
  script:
    - echo $BUILD_PROJECT_NAME # Don't. Output result: $PROJECT_NAME
    - echo $PROJECT_NAME # Do. Output result: git-cheat-sheet-and-tricks

```

### Mirroring using deploy keys

Git service providers have a mirroring functionality, allowing a repository either to push to or pull from a mirror.

However, in case mirroring is impossible due to software version or a network policy, a cron job or a CI pipeline with runners like Jenkins can be useful.

In order to register deploy keys in the target mirror, several steps are to follow:

- Firstly generate your SSH keys locally:

  ```bash
  ssh-keygen -t rsa -C "your.email@address.com" -b 4096
  ```

- Assign public key `id_rsa.pub` (from ssh-rsa to end of your email) to the target git project, option Create a new deploy key in Project Settings. Ensure  write permission is selected.

  ```bash
  # Downloads and installs xclip. If you don't have `apt-get`, you might need to use another installer (like `yum`)
  sudo apt-get install clip
  # Copies the contents of the id_rsa.pub file to your clipboard
  xclip -sel clip < ~/.ssh/id_rsa.pub
  ```

- Add the private `SSH_KEY` to the environment variable of your repository setting and let the CI/CD pipeline or your cron job does its work :).

  ```bash
  apt update && apt-get install -y openssh
  mkdir ~/.ssh
  eval `ssh-agent -s` # start ssh-agent before adding key
  cat $SSH_KEY | ssh-add - # adding ssh key without using sensitive round brackets
  echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config # no strict key checking
  git config --global user.name "Your Name"
  git config --global user.email "your.email@address.com"
  git checkout master
  git pull --unshallow origin master # pull old tree deeply to ensure we have all new changes
  git remote add remote git@github.com:new/repo.git || true
  git push -u remote master
  ```

