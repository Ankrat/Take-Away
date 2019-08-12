# GitLab CI/CD:
> _[Documentation page](https://docs.gitlab.com/ee/ci/)_

Continuous Integration works by pushing small code chunks to your application’s code base.

Continuous Delivery and Deployment consist of a step further CI,
deploying your application to production at every push to the default branch of the repository.

## Getting Started:

- GitLab CI/CD is configured by a file called .gitlab-ci.yml placed at the repository’s root.
- The scripts set in this file are executed by the GitLab Runner (which works similarly to your terminal).

### What to put in `.gitlab-ci.yml` ?

In this file, you can define :
- the scripts you want to run
- include and cache dependencies
- choose commands you want to run in sequence
- choose commands you want to run in parallel
- define where you want to deploy your app
- specify whether you will want to run the scripts automatically or manually

## Configure your CI/CD
> _[Documentation page](https://docs.gitlab.com/ee/ci/#configuration)_

|Configuration|Description|
|--- |--- |
|Pipelines|Structure your CI/CD process through pipelines.|
|Environment variables|Reuse values based on a variable/value key pair.|
|Environments|Deploy your application to different environments (e.g., staging, production).|
|Job artifacts|Output, use, and reuse job artifacts.|
|Cache dependencies|Cache your dependencies for a faster execution.|
|Schedule pipelines|Schedule pipelines to run as often as you need.|
|Custom path for .gitlab-ci.yml|Define a custom path for the CI/CD configuration file.|
|Git submodules for CI/CD|Configure jobs for using Git submodules.|
|SSH keys for CI/CD|Using SSH keys in your CI pipelines.|
|Pipelines triggers|Trigger pipelines through the API.|
|Pipelines for Merge Requests|Design a pipeline structure for running a pipeline in merge requests.|
|Integrate with Kubernetes clusters|Connect your project to Google Kubernetes Engine (GKE) or an existing Kubernetes cluster.|
|GitLab Runner|Configure your own GitLab Runners to execute your scripts.|
|Optimize GitLab and Runner for large repositories|Recommended strategies for handling large repos.|
|.gitlab-ci.yml full reference|All the attributes you can use with GitLab CI/CD.|

## Main configuration

### Pipeline

Pipelines are the top-level component of continuous integration, delivery, and deployment.

Pipelines comprise:
- Jobs that define what to run. For example, code compilation or test runs.
- Stages that define when and how to run. For example, that tests run only after code compilation.

Multiple jobs in the same stage are executed by Runners in parallel, if there are enough concurrent Runners.

If all the jobs in a stage:
- Succeed, the pipeline moves on to the next stage.
- Fail, the next stage is not (usually) executed and the pipeline ends early.

As an example, imagine a pipeline consisting of four stages, executed in the following order:

|stages    |jobs           |
|----------|---------------|
|build     |compile        |
|test      |test, test2    |
|staging   |deploy-to-stage|
|production|deploy-to-prod |

### Env variable

An environment variable is a dynamic-named value that can affect the way running processes will behave on an operating system.

|Variable|Description|
|---|---|
|ARTIFACT_DOWNLOAD_ATTEMPTS|Number of attempts to download artifacts running a job|
|CHAT_INPUT|Additional arguments passed in the ChatOps command|
|CHAT_CHANNEL|Source chat channel which triggered the ChatOps command|
|CI|Mark that job is executed in CI environment|
|CI_BUILDS_DIR|Top-level directory where builds are executed.|
|CI_CONCURRENT_ID|Unique ID of build execution within a single executor.|
|CI_CONCURRENT_PROJECT_ID|Unique ID of build execution within a single executor and project.|
|CI_COMMIT_BEFORE_SHA|The previous latest commit present on a branch before a merge request. Only populated when there is a merge request associated with the pipeline.|
|CI_COMMIT_DESCRIPTION|The description of the commit: the message without first line, if the title is shorter than 100 characters; full message in other case.|
|CI_COMMIT_MESSAGE|The full commit message.|
|CI_COMMIT_REF_NAME|The branch or tag name for which project is built|
|CI_COMMIT_REF_SLUG|$CI_COMMIT_REF_NAME lowercased, shortened to 63 bytes, and with everything except 0-9 and a-z replaced with -. No leading / trailing -. Use in URLs, host names and domain names.|
|CI_COMMIT_SHA|The commit revision for which project is built|
|CI_COMMIT_SHORT_SHA|The first eight characters of CI_COMMIT_SHA|
|CI_COMMIT_TAG|The commit tag name. Present only when building tags.|
|CI_COMMIT_TITLE|The title of the commit - the full first line of the message|
|CI_CONFIG_PATH|The path to CI config file. Defaults to .gitlab-ci.yml|
|CI_DEBUG_TRACE|Whether debug tracing is enabled|
|CI_DEPLOY_PASSWORD|Authentication password of the GitLab Deploy Token, only present if the Project has one related.|
|CI_DEPLOY_USER|Authentication username of the GitLab Deploy Token, only present if the Project has one related.|
|CI_DISPOSABLE_ENVIRONMENT|Marks that the job is executed in a disposable environment (something that is created only for this job and disposed of/destroyed after the execution - all executors except shell and ssh). If the environment is disposable, it is set to true, otherwise it is not defined at all.|
|CI_ENVIRONMENT_NAME|The name of the environment for this job. Only present if environment:name is set.|
|CI_ENVIRONMENT_SLUG|A simplified version of the environment name, suitable for inclusion in DNS, URLs, Kubernetes labels, etc. Only present if environment:name is set.|
|CI_ENVIRONMENT_URL|The URL of the environment for this job. Only present if environment:url is set.|
|CI_JOB_ID|The unique id of the current job that GitLab CI uses internally|
|CI_JOB_MANUAL|The flag to indicate that job was manually started|
|CI_JOB_NAME|The name of the job as defined in .gitlab-ci.yml|
|CI_JOB_STAGE|The name of the stage as defined in .gitlab-ci.yml|
|CI_JOB_TOKEN|Token used for authenticating with the GitLab Container Registry and downloading dependent repositories|
|CI_JOB_URL|Job details URL|
|CI_MERGE_REQUEST_ID|The ID of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_IID|The IID of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_PROJECT_ID|The ID of the project of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_PROJECT_PATH|The path of the project of the merge request if the pipelines are for merge requests (e.g. namespace/awesome-project). Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_PROJECT_URL|The URL of the project of the merge request if the pipelines are for merge requests (e.g. http://192.168.10.15:3000/namespace/awesome-project). Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_REF_PATH|The ref path of the merge request if the pipelines are for merge requests. (e.g. refs/merge-requests/1/head). Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_SOURCE_BRANCH_NAME|The source branch name of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_SOURCE_BRANCH_SHA|The HEAD sha of the source branch of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_SOURCE_PROJECT_ID|The ID of the source project of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_SOURCE_PROJECT_PATH|The path of the source project of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_SOURCE_PROJECT_URL|The URL of the source project of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_TARGET_BRANCH_NAME|The target branch name of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_TARGET_BRANCH_SHA|The HEAD sha of the target branch of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_TITLE|The title of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_ASSIGNEES|Comma-separated list of username(s) of assignee(s) for the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_MILESTONE|The milestone title of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_MERGE_REQUEST_LABELS|Comma-separated label names of the merge request if the pipelines are for merge requests. Available only if only: [merge_requests] is used and the merge request is created.|
|CI_NODE_INDEX|Index of the job in the job set. If the job is not parallelized, this variable is not set.|
|CI_NODE_TOTAL|Total number of instances of this job running in parallel. If the job is not parallelized, this variable is set to 1.|
|CI_API_V4_URL|The GitLab API v4 root URL|
|CI_PAGES_DOMAIN|The configured domain that hosts GitLab Pages.|
|CI_PAGES_URL|URL to GitLab Pages-built pages. Always belongs to a subdomain of CI_PAGES_DOMAIN.|
|CI_PIPELINE_ID|The unique id of the current pipeline that GitLab CI uses internally|
|CI_PIPELINE_IID|The unique id of the current pipeline scoped to project|
|CI_PIPELINE_SOURCE|Indicates how the pipeline was triggered. Possible options are: push, web, trigger, schedule, api, and pipeline. For pipelines created before GitLab 9.5, this will show as unknown|
|CI_PIPELINE_TRIGGERED|The flag to indicate that job was triggered|
|CI_PIPELINE_URL|Pipeline details URL|
|CI_PROJECT_DIR|The full path where the repository is cloned and where the job is run. If the GitLab Runner builds_dir parameter is set, this variable is set relative to the value of builds_dir. For more information, see Advanced configuration for GitLab Runner.|
|CI_PROJECT_ID|The unique id of the current project that GitLab CI uses internally|
|CI_PROJECT_NAME|The project name that is currently being built (actually it is project folder name)|
|CI_PROJECT_NAMESPACE|The project namespace (username or groupname) that is currently being built|
|CI_PROJECT_PATH|The namespace with project name|
|CI_PROJECT_PATH_SLUG|$CI_PROJECT_PATH lowercased and with everything except 0-9 and a-z replaced with -. Use in URLs and domain names.|
|CI_PROJECT_URL|The HTTP(S) address to access project|
|CI_PROJECT_VISIBILITY|The project visibility (internal, private, public)|
|CI_COMMIT_REF_PROTECTED|If the job is running on a protected branch|
|CI_REGISTRY|If the Container Registry is enabled it returns the address of GitLab’s Container Registry|
|CI_REGISTRY_IMAGE|If the Container Registry is enabled for the project it returns the address of the registry tied to the specific project|
|CI_REGISTRY_PASSWORD|The password to use to push containers to the GitLab Container Registry|
|CI_REGISTRY_USER|The username to use to push containers to the GitLab Container Registry|
|CI_REPOSITORY_URL|The URL to clone the Git repository|
|CI_RUNNER_DESCRIPTION|The description of the runner as saved in GitLab|
|CI_RUNNER_EXECUTABLE_ARCH|The OS/architecture of the GitLab Runner executable (note that this is not necessarily the same as the environment of the executor)|
|CI_RUNNER_ID|The unique id of runner being used|
|CI_RUNNER_REVISION|GitLab Runner revision that is executing the current job|
|CI_RUNNER_TAGS|The defined runner tags|
|CI_RUNNER_VERSION|GitLab Runner version that is executing the current job|
|CI_SERVER|Mark that job is executed in CI environment|
|CI_SERVER_HOST|Host component of the GitLab instance URL, without protocol and port (like gitlab.example.com)|
|CI_SERVER_NAME|The name of CI server that is used to coordinate jobs|
|CI_SERVER_REVISION|GitLab revision that is used to schedule jobs|
|CI_SERVER_VERSION|GitLab version that is used to schedule jobs|
|CI_SERVER_VERSION_MAJOR|GitLab version major component|
|CI_SERVER_VERSION_MINOR|GitLab version minor component|
|CI_SERVER_VERSION_PATCH|GitLab version patch component|
|CI_SHARED_ENVIRONMENT|Marks that the job is executed in a shared environment (something that is persisted across CI invocations like shell or ssh executor). If the environment is shared, it is set to true, otherwise it is not defined at all.|
|GET_SOURCES_ATTEMPTS|Number of attempts to fetch sources running a job|
|GITLAB_CI|Mark that job is executed in GitLab CI environment|
|GITLAB_USER_EMAIL|The email of the user who started the job|
|GITLAB_USER_ID|The id of the user who started the job|
|GITLAB_USER_LOGIN|The login username of the user who started the job|
|GITLAB_USER_NAME|The real name of the user who started the job|
|RESTORE_CACHE_ATTEMPTS|Number of attempts to restore the cache running a job|
|GITLAB_FEATURES|The comma separated list of licensed features available for your instance and plan|

#### Custom variables:
To create a new custom env_var variable via `.gitlab-ci.yml`, define their variable/value pair under variables:
```yml
variables:
  TEST: "HELLO WORLD"
```
#### Syntax of variables in job scripts:

To access environment variables, use the syntax for your Runner’s shell.
|Shell|Usage|
|--- |--- |
|bash/sh|$variable|
|windows batch|%variable%|
|PowerShell|$env:variable|

#### `.gitlab-ci.yml` defined variables

For example, if you set the variable below globally (not inside a job),
it will be used in all executed commands and scripts:
```yml
variables:
  DATABASE_URL: "postgres://postgres@postgres/my_database"
```

#### Priority of environment variables:

The order of precedence for variables is (from highest to lowest):

 1. Trigger variables or scheduled pipeline variables.
 1. Project-level variables or protected variables.
 1. Group-level variables or protected variables.
 1. YAML-defined job-level variables.
 1. YAML-defined global variables.
 1. Deployment variables.
 1. Predefined environment variables.

### Environment

Environments allow control of the continuous deployment of your software, all within GitLab.
GitLab CI/CD is capable of deploying your projects in your infrastructure, with the added benefit of giving you a way to track your deployments.

```yml
stages:
  - test
  - build
  - deploy

test:
  stage: test
  script: echo "Running tests"

build:
  stage: build
  script: echo "Building the app"

deploy_review:
  stage: deploy
  script:
    - echo "Deploy a review app"
    - rsync -av --delete public /srv/nginx/$CI_COMMIT_REF_SLUG
  environment:
    name: review/$CI_COMMIT_REF_NAME
    url: https://$CI_COMMIT_REF_SLUG.example.com
  only:
    - branches
  except:
    - master

deploy_staging:
  stage: deploy
  script:
    - echo "Deploy to staging server"
  environment:
    name: staging
    url: https://staging.example.com
  only:
  - master

deploy_prod:
  stage: deploy
  script:
    - echo "Deploy to production server"
  environment:
    name: production
    url: https://example.com
  when: manual
  only:
  - master
```
### Job Artifacts
Artifacts are a list of files and directories which have been created by a job once it finishes.

Job artifacts that are created by GitLab Runner are uploaded to GitLab and are downloadable as a single archive using the GitLab UI.

```yml
pdf:
  script: xelatex mycv.tex
  artifacts:
    paths:
    - mycv.pdf
    expire_in: 1 week
```
A job named pdf calls the xelatex command in order to build a pdf file from the latex source file mycv.tex.

We then define the artifacts paths which in turn are defined with the **paths keyword**.

All paths to files and directories are relative to the repository that was cloned during the build.