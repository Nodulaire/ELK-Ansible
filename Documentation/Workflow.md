# Workflow

This document aim to explain methods used for this project.

Be free to contact us at any time. Contact information are available on the main README.
Please consider using PGP to contact us. It's a good habit to take ;)




## Git
If you are a contributor, please read those instructions before merging your work.

Any time:
```
git pull  
git add (--all or the files you want to add)  
git commit -m "The reason of this commit, be verbose"
git push -u origin master (or whatever your developement branch is)
```

## Naming convention

### Playbooks

You must respect the yaml coding conventions defined below.
TODO

### Documentation

Each action realised on the project must be well documented, A project can't survive if nobody understand why its like that at any point in the time. Also we hope that someday few contributors will develop groks modules and add their work.

**Names**: %SERVICE%-%Doc-Type%-%VERSION%  
*Examples*:
- Ansible-Turorial-v2.
- Logstash-Info-v13.md

To reach as much people as possible all the documentation is written in English.

Each document will contain :
- A short introduction of thecnology
- An aim section
- As many screenshot and code snipet as possible.
