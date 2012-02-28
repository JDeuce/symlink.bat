## What is symlink.bat? ##
symlink.bat lets you create directory and file links with one command on all Windows operating systems with the following syntax:

`symlink.bat original_name linked_name`

## The old way of doing things ##
### The standard way of linking in Windows Vista/Windows 7 ###
In windows vista and windows 7, you can create native symlinks.

The command is slightly different for directories and files:

  *  Directory: `mklink /d link_name directory_name`
  *  File: `mklink link_name file_name`

Note that by default mklink requires administrator privileges. If you want to make them as a limited user you can use secpol.msc and add your user to Local Policies -> User Rights Assignment -> Create symbolic links.

### The standard way of linking in Windows XP ###
For Windows XP, creating links is a bit more difficult.

To make directory links, you can use the junction utility from here: http://technet.microsoft.com/en-us/sysinternals/bb896768.

I couldn't find a way to make symbolic file links in XP, however, I did find how to make hardlinks, and they're good enough for my purposes.
Changing the original still changes the link. The difference is deleting the original does not delete the link, the link still points to the original file.

Windows XP link commands:

  *  Directory: `junction link_name directory_name`
  *  File: `fsutil hardlink create link_name file_name`

## Installing symlink.bat ##
### In Windows Vista / Windows 7 ###
1. Drop symlink.bat into C:\windows\system32.
2. Be sure that when you run the batch, you have administrator privileges, or you have enabled the Create Symbolic Links privilege for your user (see note about secpol.msc above).

### In Windows XP ###
1. Edit the top of the batch to set xp=true.
2. Download junction.exe from here: http://technet.microsoft.com/en-us/sysinternals/bb896768.
3. Drop both symlink.bat and junction.exe into C:\windows\system32.

