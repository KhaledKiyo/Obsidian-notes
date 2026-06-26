#system
## pacman

update system

```bash
sudo pacman -Syu
```

install a package

```bash
sudo pacman -S <name>
```

remove a package

```bash
sudo pacman -R <name>
```

remove a package and its unused dependencies

```bash
sudo pacman -Rs <name>
```

search for a package

```bash
pacman -Ss <name>
```

list installed packages

```bash
pacman -Q
```

---

## navigation

print current directory

```bash
pwd
```

go into a folder

```bash
cd <folder_name>
```

go back one folder

```bash
cd ..
```

go to home directory

```bash
cd ~
```

list files and folders

```bash
ls
```

list with details and hidden files

```bash
ls -la
```

---

## files & folders

create a folder

```bash
mkdir <folder_name>
```

create nested folders

```bash
mkdir -p <folder/sub/folder>
```

create a file

```bash
touch <file_name>
```

copy a file

```bash
cp <path/to/file> <path/to/new>
```

copy a folder

```bash
cp -r <path/to/folder> <path/to/new>
```

move or rename a file or folder

```bash
mv <source> <destination>
```

delete a file

```bash
rm <file_name>
```

delete a file with confirmation

```bash
rm -i <file_name>
```

force delete a file

```bash
rm -f <file_name>
```

delete an empty folder

```bash
rmdir <folder_name>
```

delete a folder with files

```bash
rm -r <folder_name>
```

force delete a folder

```bash
rm -rf <folder_name>
```

---

## viewing files

print file contents

```bash
cat <file_name>
```

view file page by page

```bash
less <file_name>
```

print first 10 lines

```bash
head <file_name>
```

print last 10 lines

```bash
tail <file_name>
```

follow a file in real time (useful for logs)

```bash
tail -f <file_name>
```

---

## system

show running processes

```bash
htop
```

show disk usage

```bash
df -h
```

show folder size

```bash
du -sh <folder_name>
```

show memory usage

```bash
free -h
```

shutdown

```bash
sudo shutdown now
```

reboot

```bash
sudo reboot
```

---

## misc

clear the terminal

```bash
clear
```

search for a string inside a file

```bash
grep "<text>" <file_name>
```

search recursively in a folder

```bash
grep -r "<text>" <folder_name>
```

find a file by name

```bash
find <path> -name "<file_name>"
```

run previous command as root

```bash
sudo !!
```

show command history

```bash
history
```