# The littlest Jupyter Hub Group Utilities

This repository contains tools developed to facilitate creating groups
of hub users that can share files with each other both in a fixed
"published" form and a "shared" form that can be edited by anybody in
the group. These tools were developed primarily with the administration
of small groups (University Classes) in mind. The sharing mechanism is
based on the ideas discussed in this
[github issue](https://github.com/jupyterhub/jupyterhub/issues/394).

Using these tools presently requires a three step process (assuming
a working littlest jupyterhub installation with users):

1. Run the script to create the group and its shared space:
`sudo ./mkhubgrp <grpname>`. The group name should be one word. The
group `hub_<grpname>` will be created and the shared space located
at `/opt/hubshare/<grpname>`. The location was chosen so that you will not
forget about the directories if you are removing tljh.
1. Populate the group with the appropriate hub users:
`sudo gpasswd -M jupyter-userA,jupyter-userB,jupyter-userC,... hub_<grpname>`.
1. Make a symlink in each of the users' home directories to the shared
location. `sudo ./lnhubgrp <groupname>`. This will check the list of members
to the group `hub_<grpname>` and create the link in each of their
directories.

There are two subfolders within the shared folder:
1. `shared` any documents copied to this folder can be modified by all
     members of the group.
1. `published` documents created in subfolders of this folder can not be
     modified or deleted by other members of the group, only the owner.
     However, all members of the group can read and copy these documents.
     Documents should not be saved directly in the `published`
     folder because any member of the group can delete them, but not edit.
     
Hope this is useful to some. I encourage someone to integrate this into
the jupyterhub administrative web interface.

 Jonathan Gutow <gutow@uwosh.edu>
 June 2020
 license: GPLV3+