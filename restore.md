### How to restore MacBook from a backup placed on network share

1. Press Cmd + R after power on or restart your MacBook and enter into the Recovery Mode

2. Run the Terminal from the Utilities menu

3. Create a mount point for your network share and mount it
```console
mkdir /Volumes/TimeMachine
mount -t afp afp://username:password@YourServerIPAddress/ShareName /Volumes/TimeMachine
```

4. Find a sparse image with your backup, attach the image and exit from the Terminal
```console
ls -la
hdid /Volumes/TimeMachine/TimeMachine.sparsebundle
exit
```

5. Chose "Restore From Time Machine Backup" from the Recovery menu

6. Select a volume with your backup in Select a Backup Source

7. Select the backup you want to restore and chose a destination disk

##### Materials helped me

1. https://apple.stackexchange.com/questions/162544/how-to-restore-system-from-network-drive
