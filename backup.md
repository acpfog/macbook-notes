### How to make a backup to a shared folder or NAS

Officially Time Machine doesn't work with any network share, but you can backup your MacBook without buying a special network device or an external HDD. Just do a little work.

##### Connect a shared folder to your MacBook

On your home server or NAS share a folder with some access credentials.
On your MacBook open the Finder, press Cmd + K and type an address of the shared folder. Connect to the folder and store credentials in Keychain.

The folder should be accessible
```console
$ ls /Volumes/Shared_Folder
```
##### Create a sparse image

A sparse image will be a resizable virtual disk with HFS filesystem inside. A sparse image increases when you add data to it, but the Time Machine will be effectively capped by a maximum size of the image.

It's reasonable to set the size that is twice as large as the capacity of your MacBook's disk.

Make an image
```console
$ hdiutil create -size 500G -type SPARSEBUNDLE -fs HFS+J -volname "TimeMachine" TimeMachine.sparsebundle
```
##### Move the image to the network and mount it

You can drag the created image to the connected network share in the Finder or move it by command
```console
$ mv TimeMachine.sparsebundle /Volumes/Shared_Folder/
```
Now mount the image by double-clicking it on the network share in the Finder.

If everything is OK, the new "TimeMachine" drive should appear in your Finder's sidebar and it should be accessible
```console
$ ls /Volumes/TimeMachine
```
##### Backup your MacBook with Time Machine

Tell Time Machine about your new virtual drive
```console
$ sudo tmutil setdestination /Volumes/TimeMachine
```
Go to the System Preferences and open the Time Machine settings. In a case of success, you should see your virtual drive as the default destination.

Click on the Time Machine icon and select "Back Up Now" to begin the instant backup.

##### Materials helped me

1. http://www.makeuseof.com/tag/turn-nas-windows-share-time-machine-backup/
2. http://www.makeuseof.com/tag/backup-mac-homemade-time-capsule/
3. http://osxdaily.com/2010/07/21/how-to-do-manual-backups-with-time-machine/
