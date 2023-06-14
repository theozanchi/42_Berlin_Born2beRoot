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

## LVM
VM stands for Logical Volume Management. It is a system of managing logical volumes, or filesystems, that is much more advanced and flexible than the traditional method of partitioning a disk into one or more segments and formatting that partition with a filesystem.

Here’s why LVM is used and what benefits it brings:

1. **Flexibility in Managing Storage**: With LVM, you can create logical partitions that can span across multiple physical disks. This is useful in situations where a partition might run out of space, and you need to add more without going through the hassle of reformatting disks.
2.** Easy to Resize Partitions**: You can quickly and easily resize logical volumes, even while they are in use. This means that if a particular partition needs more or less space, you can resize it without any downtime
3. **Snapshots**: LVM allows you to create snapshots of your logical volumes. This means that you can create an exact copy of a volume's contents at a particular point in time. This is extremely useful for backups or for testing changes before deploying them to a production environment
4. **Disk Encryption**: LVM can be combined with disk encryption methods to encrypt logical volumes. This is sometimes easier and more flexible than encrypting physical partitions
5. **Performance Enhancement**: Through striping, you can enhance the performance of the system by spreading data across multiple disks. This can result in higher data throughput compared to using a single disk
6. **Multiple Physical Devices Management**: LVM allows you to manage multiple physical devices such as hard disks or SSDs as a single group of storage
7. **Replacing Disks**: If you need to replace a disk, LVM makes the process much easier. You can move the logical volumes to a new disk and remove the old one without much hassle

To sum it up, LVM provides a layer of abstraction between your operating system and the physical disks. This abstraction makes it much easier to manage disk space. If you run out of space on a logical volume, you can simply add a new disk to the volume group, and extend the logical volume to use this new space, without any need to move data around or repartition. This makes LVM a very powerful tool for managing disk space on Linux systems, particularly in environments where storage requirements change often.

## SSH
SSH stands for Secure Shell. It is a cryptographic network protocol used for securely accessing network services over an unsecured network, such as the internet. SSH is widely used for logging into and executing commands on remote servers, and for securely transferring files between systems.

Here are the key aspects of SSH and reasons for its widespread use:

1. **Encryption**: SSH encrypts data transmitted over the network. This means that even if the data is intercepted, it cannot be read without the encryption keys. This is crucial for protecting sensitive data and communications from eavesdropping
2. **Authentication**: SSH uses public key cryptography for authenticating users and hosts. A user can prove their identity to an SSH server using a cryptographic key pair (public and private key). Additionally, the client can verify the identity of the SSH server, which protects against man-in-the-middle attacks
3. **Integrity**: SSH ensures the integrity of the data being transmitted. It uses cryptographic hashes to make sure that the data hasn't been altered in transit. If the data is tampered with, the hashes will not match, and the recipient will know that the data has been compromised
4. **Confidentiality**: By keeping the data encrypted, SSH ensures that sensitive information remains confidential. This is essential in scenarios where passwords or other confidential data need to be sent over the network
5. **Secure File Transfer**: SSH includes the functionality for secure file transfer via protocols like SFTP (SSH File Transfer Protocol) or SCP (Secure Copy Protocol). This is often used for securely transferring files to and from remote servers
6. **Tunneling**: SSH can be used to create a secure tunnel between machines through which data can be sent securely. This is often used for securely accessing network resources that might not be directly accessible over the internet.
7. **Remote Command Execution**: SSH allows for executing commands on a remote server. This is especially useful for system administrators who need to manage servers without physically being at their location
8. **Port Forwarding**: SSH can forward arbitrary TCP ports over the encrypted channel. This can be used for securely accessing services (like a database) on the remote machine which is not exposed to the internet
9. **Replacement for Insecure Protocols**: Before SSH, protocols like Telnet and FTP were used for remote login and file transfers, respectively. However, these protocols transmit data, including passwords, in plaintext. SSH was developed as a secure alternative to these insecure protocols.

In summary, SSH is an essential tool for secure communications and is widely used in a variety of applications including remote server management, secure file transfers, and creating secure communication channels over unsecured networks.
