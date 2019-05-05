# modules
Demo to check out submoduling

I would assume this is useful for microservices, where you have a git repo for every docker container that functions as a microservice.
Each project is a main module, with helm charts that depend on the submodules and integration tests. Each microservice is a submodule, with source code, unit tests, jenkinsfile and helm charts.

Within spinnaker, every git module push triggers a pipeline. The main projects pipeline is simply all those pipelines combined.

It is currently not possible to version control the pipelines of spinnaker:
https://www.spinnaker.io/community/faqs/#how-do-i-store-my-spinnaker-application-in-version-control


### Git submodules CLI 101
`git submodule add git@github.com:mrasap/subModuleA.git`   
Will add the repo mrasap/subModuleA as a submodule. This will be shown in the .gitmodules file. 
The repo is only shown as a directory, you need to init it first if you want the code.

`git submodule update --remote --merge`   
Remote flag will also check remote, merge flag will automatically merge the updates.

`git push --recurse-submodules=on-demand`   
Push changes of a submodule while in the main module directory. 
Alternatively, you can also cd into the submodule and your git commands are automatically applied to the submodule. 

`git submodule foreach '<<YOUR GIT COMMAND>>'`   
This will apply the git command for each individual submodule. For instance:    
`git submodule foreach 'git checkout -b newFeature'`   
will create a new branch named 'newFeature' and switch to it in each individual submodule.   

**To clone a repo with submodules**:   
`git clone git@github.com:mrasap/modules.git`   
This will clone this module, but the submodules will only be shown as a directory.   

`git submodule init`   
This will init the submodules for you.   

Alternatively, you could also clone the main module and all submodules in one command:   
`git clone --recurse-submodules git@github.com:mrasap/modules.git`


### useful aliases

```
$ git config alias.sdiff '!'"git diff && git submodule foreach 'git diff'"
$ git config alias.spush 'push --recurse-submodules=on-demand'
$ git config alias.supdate 'submodule update --remote --merge' 
```
With these aliases, you can simply `git spush` to push into all submodules.


### source
https://git-scm.com/book/en/v2/Git-Tools-Submodules
