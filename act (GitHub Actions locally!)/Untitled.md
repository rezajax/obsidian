

reza@pc:~/IdeaProjects/exposd$ act list
INFO[0000] Using docker host 'unix:///var/run/docker.sock', and daemon socket 'unix:///var/run/docker.sock' 
? Please choose the default image you want to use with act:
  - Large size image: ca. 17GB download + 53.1GB storage, you will need 75GB of free disk space, snapshots of GitHub Hosted Runners without snap and pulled docker images
  - Medium size image: ~500MB, includes only necessary tools to bootstrap actions and aims to be compatible with most actions
  - Micro size image: <200MB, contains only NodeJS required to bootstrap actions, doesn't work with all actions

Default image and other options can be changed manually in /home/reza/.config/act/actrc (please refer to https://github.com/nektos/act#configuration for additional information about file structure)  [Use arrows to move, type to filter, ? for more help]
  Large
> Medium
  Micro


---

reza@pc:~/IdeaProjects/exposd$ act --list
INFO[0000] Using docker host 'unix:///var/run/docker.sock', and daemon socket 'unix:///var/run/docker.sock' 
Stage  Job ID   Job name  Workflow name           Workflow file  Events
0      build    build     Build and Release JAR   publish.yml    push  
0      build    build     Build and Release JAR2  publish2.yml   push  
1      release  release   Build and Release JAR   publish.yml    push  
1      release  release   Build and Release JAR2  publish2.yml   push  

Detected multiple jobs with the same job name, use `-W` to specify the path to the specific workflow.
reza@pc:~/IdeaProjects/exposd$ 
