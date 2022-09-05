# Windows Explorer: Changing Group Display Name

For a given registry key, change the value of `(Default)` key to the desired
group name.

eg. for `HKEY_LOCAL_MACHINE\SOFTWARE\Classes\VLC.flv`, changing the
`(Default)` key to "Flash Video" moves it above "Video File (.avi)"
alphabetically in Windows Explorer.

## Example registry keys

```windows-registry-keys
HKEY_LOCAL_MACHINE\SOFTWARE\Classes\mplayerc.avi
HKEY_LOCAL_MACHINE\SOFTWARE\Classes\mplayerc.flv
HKEY_LOCAL_MACHINE\SOFTWARE\Classes\VLC.avi
HKEY_LOCAL_MACHINE\SOFTWARE\Classes\VLC.flv
```
