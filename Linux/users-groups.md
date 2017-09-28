Creating Users and Groups
=========================

In this exercise you will create new users in a few different ways, and see how they differ. The exercise will make a lot more sense if you have read Chapter 14 in the textbook: *Creating Users and Groups*.

The three different techniques we'll use to create users are:

* the default Ubuntu User Accounts tool
* the GNOME Users and Groups tool
* the shell

Just for fun we'll also create a couple of groups and assign users to them.


1. Prerequisite
---------------

If you haven't already done so, read the tip *Managing Users and Groups the Gooey (GUI) Way*. It describes the two different GUI tools, when to use each one, and how to install the GNOME Users and Groups tool.


2. Create Users with GUI Tools
------------------------------

We are going to have a system full of users named Amy, but created using different methods. In order to tell them apart, the fourth character of the user name will be either 'u' (for Ubuntu) or 'g' (for GNOME), and the fifth character will be either 's' (for Standard user) or 'a' (for Administrator).


### 2.1 Ubuntu User Accounts Tool

Start the Ubuntu User Accounts tool, located here on the GNOME desktop: Applications > System Tools > Administration > User Accounts. (If you are using the Unity desktop, click on the Dash icon in the upper-left corner, then type in "user" and click on the User Accounts icon when it is displayed.) In order to create new users, you'll first have to click on the Unlock button in the upper-right corner. Then click on the "+" button in the lower-left corner to create a new user. Create the following two users with the Ubuntu User Accounts tool:

* `amyus` is a standard user, with full name Amy Ubuntu Standard
* `amyua` is an administrator, with full name Amy Ubuntu Admin

If you are dying of curiosity to see what happened -- and admit it, you are -- then look at the last two lines of file `/etc/passwd` (with the `tail` command, for example) to see the records you just created. They should look something like this:

    amyus:x:1001:1001:Amy Ubuntu Standard,,,:/home/amyus:/bin/bash
    amyua:x:1002:1002:Amy Ubuntu Admin,,,:/home/amyua:/bin/bash


### 2.2 GNOME Users and Groups Tool

Create similar users with the GNOME Users and Groups tool. Start the tool here on the GNOME desktop: Applications > System Tools > Administration > Users and Groups. (If you are *still* using the Unity desktop, use Dash again.)

Note that creating these users requires choosing the user name, setting an initial password (you can use the same password for all of them), and then after the account has been created as account type Custom, click on "Change..." to change the account type to either Administrator or Desktop user. Create these users:

* `amygs` is a standard/desktop user, with name Amy GNOME Standard
* `amyga` is an administrator, with name Amy GNOME Admin

The last two lines of `/etc/passwd` should now look something like this:

    amygs:x:1003:1003:Amy GNOME Standard,,,,:/home/amygs:/bin/bash
    amyga:x:1004:1004:Amy GNOME Admin,,,,:/home/amyga:/bin/bash


3. Create a Standard User with the Shell
----------------------------------------

Now let's create a standard user with the shell. The command you'll want to use is `useradd`. Chapter 14 in our textbook contains all the info you need to know to create and modify users and groups via the shell.

Create a new user and don't provide any options. Call the user `amysd`, which means a user created with the shell, using defaults. (Possibly relevant question: Can mere mortals create new users?)


4. Examine the New Users
------------------------

Take a look at the five users you have created. Some things you can look at are:

* What do their entries in `/etc/passwd` look like?
* Was a home directory created in `/home` for each of them? (Don't blindly trust what `/etc/passwd` says.)
* What groups do they already belong to? (Use the `id` command, for example: `id amyga`.)

Compare the two administrators with each other. Compare the three standard users. What differences do you see?

The admins created with the two GUIs do not belong to all the same groups. Also, the standard users do not all belong to the same groups. How do you explain this?

Answer: The Ubuntu User Accounts tool knows specifically how to create users for Ubuntu. However the GNOME Users and Groups tool is a generic tool that works on various Linux distributions, and it doesn't know about the specific groups that (for example) an Ubuntu admin should belong to.


5. Create a "Better" User via the Shell
---------------------------------------

You may have noticed that `amysd`, a default standard user created with the shell, has the following three differences from those standard users created with the GUI tools:

1. Her `/etc/passwd` entry does not have a comment.
2. Her `/etc/passwd` entry does not have a login shell.
3. A home directory was not created, even though `/etc/passwd` says it exists.

If you didn't notice these differences then maybe you are going too fast. ;-) In any case, we want to correct this totally unacceptable state of affairs.

Do the following steps. You will find the options documented either in the book or on the `man` pages for the `useradd` and `usermod` commands:

1. Use the `useradd` command to create new user `amyso` (**s**tandard user with **o**ptions). Explicitly tell the command to *create* the home directory. The book says this is the default. The book is wrong (as we have just seen with user `amysd`.) Note: You do *not* want to specify the option that specifies *where* to create the home directory; we are quite happy with `/home`.

2. Once user `amyso` has been created, modify the user to have comment "Amy Shell Options" and the same login shell as the other users. The sample command below shows the options we would use to modify hypothetical user `schmoe`:

    sudo usermod --comment "Joe Schmoe" --shell /bin/oyster schmoe

When you are done, the last six lines of `/etc/passwd` should look something like this:

    amyus:x:1001:1001:Amy Ubuntu Standard,,,:/home/amyus:/bin/bash
    amyua:x:1002:1002:Amy Ubuntu Admin,,,:/home/amyua:/bin/bash
    amygs:x:1003:1003:Amy GNOME Standard,,,,:/home/amygs:/bin/bash
    amyga:x:1004:1004:Amy GNOME Admin,,,,:/home/amyga:/bin/bash
    amysd:x:1005:1005::/home/amysd:/bin/sh
    amyso:x:1006:1006:Amy Shell Options:/home/amyso:/bin/bash


6. Create Groups and Assign Members
-----------------------------------

Finally, create two groups and add members, using whatever technique you choose.

If you choose to use the GUI method, recall that only one of the GUI tools can manage groups. Members are managed via the group.

If you choose to use the shell, you will use a group command to create the group, then a user command to modify the groups the user belongs to. Hint: When modifying what groups the user belongs to, be sure to include the `-a` option to *append* new groups to the user's current groups instead of *replacing* them.

The groups and members should be the following:

1. Create group `ubuntugrp`. Members of this group should be users you created using the Ubuntu User Accounts tool.
2. Create group `gnomegrp`. Members of this group should be users you created using the GNOME User and Group tool.

You can double-check your work by looking at the last two lines of `/etc/group`. They should look something like this:

    ubuntugrp:x:1006:amyua,amyus
    gnomegrp:x:1007:amygs,amyga