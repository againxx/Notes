# File System Hierarchy

Linux system directories typically contain three part
* Scope
* Category
* Application

![three parts](https://gitee.com/againxx/image-storage/raw/master/images/20210911082920.png =750x)

## Category part
#### Categories for programs
* _bin_: Programs (usually binary files)
* _sbin_: Programs (usually binary files) intended to be run by the superuser
* _lib_: Libraries of code used by programs

#### Categories for documentation
* _doc_: Documentation
* _info_: Documentation files for emacs's built in help system or **info** program
* _man_: Documentation files (manual pages) displayed by the **man** program; the files are often compressed and are sprinkled with typesetting commands for man to interpret
* _share_: Program-specific files, such as examples and installation instructions (cmake modules)

#### Categories for configuration
* _etc_: Configuration files for the system (and other miscellaneous stuff)
* _init.d_: Configuration files for booting Linux ( **init** )
* _rc.d_: Configuration files for booting Linux; also rc1.d, rc2.d, ...

#### Categories for programming
* _include_: Header files for programming
* _src_: Source code for programs

#### Categories for web files
* _cgi-bin_: Scripts/programs that run on web pages
* _html_: Web pages
* _public_html_: Web pages, typically in user's home directories
* _www_: Web pages

#### Categories for display
* _fonts_: Fonts
* _X11_: X window system files (more like a application part than category)

#### Categories for hardware
* _dev_: Device files for interfacing with disks and other hardware
* _media_: Mount points, directories that provide access to disks (automatically mounted disks)
* _mnt_: Mount points, directories that provide access to disks (manually mounted disks)

#### Categories for runtime files
* _var_: Files specific to this computer, created and updated as the computer runs
* _lock_: Lock files, the existence of a lock file may prevent another program, or another instance of the same program, from running or performing an action
* _log_: Log files that track important system events, containing error, warning, and informational messages
* _mail_: Mailboxes for incoming mail
* _run_: PID files, which contains IDs of running processes; these files are often consulted to track or kill particular process
