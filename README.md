# modules
Demo to check out submoduling

I would assume this is insanely useful for microservices, where you have a git repo for every docker container that functions as a microservice.
Each project is a main module, with helm charts that depend on the submodules. Each microservice is a submodule, with source code, jenkinsfile and helm charts.

Within spinnaker, every git module push triggers a pipeline. The main project is simply all those pipelines combined together.

It is currently not possible to version control the pipelines of spinnaker:
https://www.spinnaker.io/community/faqs/#how-do-i-store-my-spinnaker-application-in-version-control

### source
https://git-scm.com/book/en/v2/Git-Tools-Submodules
