# Working with File Links: Notesheet

- _Soft link_: (AKA Symlink)

  - For both directories and files.
  - Can span across file systems.
  - Points to a target file _name_, not its contents.
  - Breaks if the target file moves, or is deleted.

- _Hard link_:

  - For files on the same file system only.
  - Points to the same inode as the target file. Even if the original target
    file is deleted, the data will still be accessible via hard links - as the
    underlying inode will not be deleted until all references to it are removed.

## Windows `MKLINK`

### File soft link

```cmd
mklink "name" \\remote\file
```

### Directory soft link

```cmd
mklink /d "name" \\remote\dir
```

### [Safe removal](https://superuser.com/questions/167076/how-can-i-delete-a-symbolic-link)

Deleting the link via explorer leaves the target directory unmodified ie. avoids
accidentally deleting directories and/or their contents

---

## UNIX `ln`

### Soft link

```shell
ln -s /target/dir
```

### Hard link

```shell
ln /target/file
```

### [Safe removal](http://osxdaily.com/2016/05/25/how-delete-symbolic-link-symlink/)

```shell
unlink symlink
```

---

[File Linking](https://unix.stackexchange.com/a/23251)
