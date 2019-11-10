# KVM-backup
Backup KVM VMs

Most recent version slightly changes the syntax. It is now:

backup_VM VM_Name Full_Path_VM_Drive_Location BackupLocation

ie:

backup_VM Fedora30_container_from_yaml /media/NotHome/VMs/container_server.qcow2 /media/NotHome/VMs/backups

First stops it because backing up a running VM can lead to an unusable backup.

Then it copies the drive specified to the backup location under a folder named "current". 

It dumps the current XML that can be used to recreate this VM to the same folder.

It creates a a tar file in the backup folder and then clears the current folder. This way if you run it from a cron job, it's not going to keep adding to the same tar file.

Then it turns the VM back on.

Current limitations: if the VM has more than one drive, only the one specified will be copied. Will probably move on to using the python libvirt bindings to create a more robust backup in the future.
