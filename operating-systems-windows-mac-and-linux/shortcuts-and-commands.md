# Shortcuts and Commands

* [ ] Describe the various useful keyboard shortcuts provided by Windows.
* [ ] Describe various useful Windows keyboard shortcuts.

## Windows Shortcuts

Common tasks that can be accessed using the Windows or Ctrl Key and another key.

* Time saving and helpful for tasks done regularly.

Ctrl+Z : Undo will roll back your last action.

Ctrl+W : Will close down whatever viewing.

Ctrl+A : Select all allows to highlight all of the text in a document or select all of the files in a folder.

Alt+Tab : Switch apps by scrolling through all the windows quickly.

Alt+F4 : Shuts down active apps to skip the process of hunting for the on-screen menus.

Win+D : Minimizes all open windows, bringing desktop to view.

Win+Left Arrow or Win+Right Arrow : Snapping a window simply opens it on one side of the screen (left or right).

Win+Tab : Similar to Alt+Tab, allows to switch between apps by opening task view application switcher.

Tab and Shift+Tab : Move backward and forward through options, saving a click on mouse.

### Additional Shortcuts

F2 : Rename a highlighted file and allows to edit text in other programs.

F5 : Refresh a page on web browser.

Win+L : Locks the machine and returns to the login screen.

Win+I : Open settings dialog for Windows.

Win+S : The Windows taskbar to directly search through applications and saved files.

Win+PrtScn : Save a screenshot of the whole screen and saves it as a PNG file in the Screenshots folder. At the same time, Windows will copy the image to the clipboard.

* Alt+PrtScn will take a screenshot of just the active window and will only copy the image to the clipboard.

Ctrl+Shift+Esc : Opens the Task Manager from wherever you are and whatever application is running.

* The Task Manager is a window into everything running on Windows system, from the open programs to the open background processes.

Win+C : Activate Cortana from the taskbar search box.

Win+D : Creates a new virtual desktop. Virtual desktops create secondary screens to organize open applications and windows to provide extra workspace.

Win+X : Open Quick Link menu to access all key areas of the system.

## Linux Basic Commands

What do these useful Linux commands do:

* [ ] cd
* [ ] cp
* [ ] mv
* [ ] ls
* [ ] df
* [ ] kill
* [ ] rm
* [ ] rmdir
* [ ] cat
* [ ] mkdir
* [ ] ifconfig
* [ ] locate
* [ ] tail
* [ ] less
* [ ] more
* [ ] nano
* [ ] chmod
* [ ] Describe the basic Linux file and directory permission structure.

***

### Basic Commands

#### cd

Changes the directory where the user is currently located.

#### cp

Copies files or directories.

#### mv

Moves files or directories

#### ls

Lists information related to files and directories, like owner and privileges.

#### df

Displays file system disk space.

#### kill

Used to "kill" or stop an executing process.

#### rm

Deletes file and directories.

#### rmdir

Deletes an empty directory.

#### cat

Short for concatenate. It can combine several files into one. Also used to see content of a file.

#### mkdir

Creates a new directory.

#### ifconfig

Used to view or configure network interfaces.

#### locate

Quickly searches for the locations of files. It uses an internal database that is updated using the updatedb command.

#### tail

Views the end of a text file, by default the last 10 lines.

#### less

Efficient while viewing huge log files as it does not need to load the full file while opening.

#### more

Displays text, one screen at a time.

#### nano

A basic text editor.

#### chmod

Changes privileges for a file or directory.

***

### Permissions and Owners

![Permissions](http://linux-blog.org/wp-content/uploads/2009/09/permissions.png)

* There are three groups that can "own" a file.
  * User, group, everybody.
* For each group, there are also three types of permissions: Read, Write, Execute.
* Read: 4 (100), Write: 2 (010), Execute: 1 (001).

#### Permissions Visualized

![Permissions](https://miro.medium.com/max/2112/0\*TJYlcsbddAMcxEOt)

#### Change Permission

Use the `chmod` command to change the permissions of a file or directory.

* `chmod <permissions><filename>`
* `chmod 755 <filename>`
* `chmod u=rw,g=r,o=r <filename>`

Change owner and group owner of a file with the `chown` command.

* `chown <user>:<group> <filename>`

