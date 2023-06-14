## `sudo`

Sudo stands for switch user do and is used to use root privileges for special operations by some users

## `aptitude` amd `apt`
`aptitude` and `apt` are both command-line interfaces for the package management system on Debian-based Linux distributions such as Ubuntu.

### `aptitude`
`aptitude` is a high-level interface that can be used in both a terminal (CLI) and in a graphical environment.
It has an ncurses interface for terminal usage where you can navigate through the package listing, mark packages for installation or removal, and perform the actions, all within the interface.
It is known to handle complex package dependencies more effectively than `apt`.
It keeps a detailed log of installed packages which can be useful to track the system's package changes.
aptitude is not installed by default on many Debian-based systems, so you might need to install it separately using `sudo apt-get install aptitude`.

### `apt`
apt is also a high-level package management interface but it is optimized for interactive use in the terminal.
It is more streamlined and user-friendly than `apt-get` with colorized output, progress bars, etc.
`apt` combines the most commonly used features and options of `apt-get` and `apt-cache`, providing a simpler way to install, remove, and upgrade packages.
`apt` is installed by default on Debian-based systems and is the recommended way for installing packages interactively.

In summary, both `aptitude` and `apt` are high-level interfaces to Debian's package management system. `apt` is more streamlined and user-friendly, while `aptitude` has an optional text-based user interface and some features for handling complex dependencies.

## AppArmor
AppArmor (Application Armor) is a Linux security module that provides mandatory access control (MAC) for programs. It allows the system administrator to restrict programs' capabilities with per-program profiles. Profiles can allow capabilities like network access, raw socket access, and the permission to read, write, or execute files on matching paths.

AppArmor's security model is to bind access control attributes to programs rather than to users. This is used to confine programs to a limited set of resources, which can prevent exploitation of software flaws and compromised systems.

Some key points of AppArmor are:

It protects the operating system and applications from external or internal threats.
AppArmor's profiles can be in enforcing mode, which enforces the policy defined in the profile, or complain mode, which only logs policy violations without enforcing them.
It is designed to be easier to build and maintain than SELinux (another Linux security module) as it uses a simpler security policy with fewer fine-grain controls.
AppArmor is integrated into the Linux kernel and does not require any additional daemons running.
AppArmor is particularly common in Ubuntu systems and is used as an alternative to SELinux which is common in Red Hat-based systems.
