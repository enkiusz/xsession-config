# Very simple (though not simplistic) xsession launching set of scripts

These scripts are used to setup and launch a Xorg session preferably using 
one of the simple tab-based window managers like i3 or xmonad. This is
because bigger desktop environments like KDE or Gnome will have their own
scripts and processes handling session setup.

The installation is very simple, all of the files in the repository should be
put in the home directory of the user either via stow/xstow or plain copying
(not recommended though).

The configuration contains the following directories:

```
➜  ~ tree -a ~/stow/xsession/    
/home/enki/stow/xsession/
├── .config
│   └── xsession
│       ├── common
│       │   ├── systemd-logind-idle-hint
│       │   └── watch-xss-status
│       ├── session-active.d
│       │   └── 50systemd-logind-idle-hint -> ../common/systemd-logind-idle-hint
│       ├── session-idle.d
│       │   ├── 50detach-usbip-devices
│       │   └── 50systemd-logind-idle-hint -> ../common/systemd-logind-idle-hint
│       ├── xprofile.d
│       │   ├── 10-local-path
│       │   └── 50-pl-keymap
│       └── xsession.d
│           ├── 50redshift
│           ├── 50xrandr
│           ├── 50xscreensaver
│           ├── 50xsetroot
│           └── 999wm
├── README.md
├── .xprofile
└── .xsession

7 directories, 15 files
```

The common/ directory contains common scripts that can be accessed when the session
is being setup as well as later. The common/ directory is being appended to the 
system PATH.

The xprofile.d and xsession.d are a run-parts style directories containing various scripts
and commands used to setup the Xorg session. The difference between those two places is that
files from xprofile.d are sourced to the interpreter handling the session setup (xinit).

session-idle.d and session-active.d directories contain scripts which are launched when a 
idle condition on the state is detected.

