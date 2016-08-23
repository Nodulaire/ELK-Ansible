# Workflow

|  Date | Version  | Author  | Change/Addition  |
|---|---|---|---|
| 23/08/2016  | 1 | Nodulaire  |  Compliance  |

The aim of the document is to explain the methods used for this project.

Be free to contact us at any time. Contact information are available on the main [README](..//README.md).
Please consider using PGP to contact us. It's a good habit to take ;)


## Summary
1 - [Git](#git)  
2 - [Namimg convention](#naming-convention)  
2.1 - [Playbooks](#playbooks)  
2.2 - [Documentation](#documentation)   

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

You must respect the *yaml* coding conventions defined below.  
Each playbooks start with ```---```. Then we have to indicate the hosts on which we want to deploy the playbook. After we decline all playbook's tasks.
Here the entire structure:  
```
---
- hosts : NAME
  tasks :
    - name : Task's description
    ...
    - tags : [Tag's name]
```

Here *NAME* refers to the cluster of machines define in */etc/ansible/hosts*. You have an example of the configuration in [hosts](../../Playbooks/hosts).  
The tag *tags* is optional, but it should be useful for debugging.  
Then the *...* is the command you want to execute.  
Finally the *(...)* means the end of the playbook they are optional.

### Documentation

Each action realised on the project must be well documented, A project can't survive if nobody understands why its like that at any point in the time. Also, we hope that someday few contributors will develop groks modules and add their work.

**Names**: %SERVICE%-%Doc-Type%-%VERSION%  
*Examples*:
- Ansible-Turorial-v2.
- Logstash-Info-v13.md

To reach as many people as possible all the documentation is written in English.


Each document will contain :
- A short introduction of technology
- An aim section
- As many screenshot and code snippets as possible.





That's all folks !  
Thanks for reading,  
**Nodulaire**
