# PERMISSIONS
1. `Add` permission directory to a user
```vim
sudo setfacl -m u:<username>:rw <directory>
```
2. `Check` permissions a directory

```vim
getfacl <directory>
```