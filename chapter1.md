# CHAP 1
## 1. Terms and Concepts
- Binaries: tập thực thi, nằm trong /usr/bin và /usr/sbin tương tự như file (.exe) trong windows.
- Case sensitivity: Desktop khác desktop.
- Directory: folder.
- Home: mỗi user có /home directory khác nhau.
- root: superuser account.
- Dùng Python, bashshell.
- Terminal: command line interface.

**passwd: change password**

## 2. The linux file system
- Linux không có drive vật lý như C mà dùng logical filesystem. Cao nhất là /

## 3. Basic Commands in Linux
- pwd: returns your location within the directory structure.
- whoami: checking your login
- cd: change directories, using double dots (..) to move up one level
- ls: listing the contents of a dicrectory, -l to get more information, -la to show hidden files.

--help / -h / -?: provides guidance for aplication's use.
- man appname: a manual page with more information

## 4. Finding Stuff:
- locate <keyword>: this command will go through entire filesystem and locate every occurrence of that word => overwhelming. And locate uses a database that is only updated once a day.
- whereis <keyword>: looking for a binary file.
- find directory options expression
Ex: find / -type f -name apche2
/: bắt đầu từ thư mục gốc
-type f: file thông thường
-name apache2: tên tệp cần tìm.

- A search that looks in every directories -> slow. In this case we are looking for a configuration file, so we can start in /etc directory.

=> find /etc -type f -name apache2

- find displays only exact name matches. If the file apache2 has an extension, using wildcards
Ex: find /etc -type f -name apache2.*

- ps aux: to display information about processes running on the machine.

- grep: as a filter to search for keywords.

Ex: I just want to find one process to see if it is running. I can do this piping the output from ps to grep and searching for a keyword. for instance, to find out whether the apache2 service is running

=> ps aux | grep apache2

## 5. Modifying Files and Directories

**1. Small file**
cat > filename: and then you can be begin typing. To exit, press CTRL + D. This command can be overwrite the file with new information

cat filename: to see what's in the file filename.

cat >> filename: to add, append more content to a file.

**2. Creating a File**
touch newfile

**3. Creating a Directory**
mkdir newdirectory

**4. Copying a File**
cp oldfile /root/newdirectory/newfile

Copying oldfile and renaming the file is newfile

**5. Renaming a file**
mv command can be used to move a file/dir to a new location or simply give an existing file a new name.

mv newfile newfile2

**6. Removing a file**
rm filename

**7. Removing a Directory**
rmdir dirname: rmdir won't remove a dir that isn't empty. You can use the -r switch to remove a dir and its content all in one go

rm -r dirname