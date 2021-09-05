Ich wollte einen ESXi auf 6.5 U1 upgraden – doch das Upgrade auf einem USB-Stick installierten Server ist mit folgender Fehlermeldung abgebrochen:

>[InstallationError]
>Failed updating the bootloader: Execution of command /usr/lib/vmware/bootloader-installer/install-bootloader failed: non-zero code returned
>return code: 1
>output: ERROR: ld.so: object ‚/lib/libMallocArenaFix.so‘ from LD_PRELOAD cannot be preloaded: ignored.
>Traceback (most recent call last):
>File „/usr/lib/vmware/bootloader-installer/install-bootloader“, line 238, in
>main()
>File „/usr/lib/vmware/bootloader-installer/install-bootloader“, line 223, in main
>partType, diskGeom, parts = getDiskInfo(diskPath)
>File „/usr/lib/vmware/bootloader-installer/install-bootloader“, line 151, in getDiskInfo
>rc, out, err = execCommand(command)
>File „/usr/lib/vmware/bootloader-installer/install-bootloader“, line 94, in execCommand
>raise Exception(„%s failed to execute: status(%d)“ % (command, process.returncode))
>Exception: /sbin/partedUtil getptbl /vmfs/devices/disks/naa.200049454505080f failed to execute: status(255)
>vibs = VMware_bootbank_esx-base_6.5.0-1.26.5969303
>Please refer to the log file for more details.

Ich habe das Problem mit dem deaktivieren des neuen USB-Treibers gelöst:

```console
esxcli system module set -m=vmkusb -e=FALSE
```

danach reboot und dann nochmal das Upgrade versucht -> funktioniert.

Nach dem erfolgreichen Upgrade sollte man den Treiber wieder mit

```console
esxcli system module set -m=vmkusb -e=TRUE
```

aktivieren.

Nach einem weiteren Reboot ist man dann wieder up-to-date 🙂
