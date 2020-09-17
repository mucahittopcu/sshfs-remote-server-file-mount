
# SSHFS Remote Server File Mount
[![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/colored.png)]()

SSHFS is a file system client used to connect and interact with directories and files over a regular ssh connection located on a remote server or workstation.

## Installing SSHFS

```sh
sudo apt-get install sshfs
```

## Mounting the Remote File System
To start we will need to create a local directory in which to mount the droplet’s file system.
```sh
sudo mkdir /mnt/folder_name
```

Now we can use sshfs to mount the file system locally with the following command. If your VPS was created with a password login the following command will do the trick. You will be asked for your virtual server’s root password during this step.

```sh
sudo sshfs -o allow_other,default_permissions root@xxx.xxx.xxx.xxx:/ /mnt/folder_name
```

##Unmounting the Remote File System
When you no longer need the mount point you can simply unmount it with the command



```sh
sudo umount /mnt/folder_name
```
##Permanently Mounting the Remote File System
SSHFS also allows for setting up permanent mount points to remote file systems. This would set a mount point that would persist through restarts of both your local machine and droplets. In order to set up a permanent mount point, we will need to edit the /etc/fstab file on the local machine to automatically mount the file system each time the system is booted.

First we need to edit the **/etc/fstab** file with a text editor.


```sh
sudo nano /etc/fstab
```
Scroll to the bottom of the file and add the following entry

```sh
sshfs#root@xxx.xxx.xxx.xxx:/ /mnt/folder_name
```
Save the changes to /etc/fstab and reboot if necessary.

**NOTE :** It should be noted that permanently mounting your VPS file system locally is a potential security risk. If your local machine is compromised it allows for a direct route to your droplet. Therefore it is not recommended to setup permanent mounts on production servers.

<hr>

- **[SOURCE](https://www.digitalocean.com/community/tutorials/how-to-use-sshfs-to-mount-remote-file-systems-over-ssh)**