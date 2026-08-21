# Day 10 – File Permissions & File Operations

## Task 1: Create Files

* Created `devops.txt` using `touch`
* Created `notes.txt` using `echo`
* Created `script.sh` using `vim`
* Verified using `ls -l`

## Task 2: Read Files

* Used `cat` to read `notes.txt`
* Used `vim -R` to view `script.sh`
* Used `head -n 5 /etc/passwd`
* Used `tail -n 5 /etc/passwd`

## Task 3: Permissions

Linux permissions are:
`r = 4`, `w = 2`, `x = 1`

Checked permissions using:

```bash
ls -l devops.txt notes.txt script.sh
```

## Task 4: Modify Permissions

```bash
chmod +x script.sh
chmod -w devops.txt
chmod 640 notes.txt
mkdir project
chmod 755 project
```

Ran the script using:

```bash
./script.sh
```

## Task 5: Permission Testing

* Writing to a read-only file → **Permission denied**
* Running a file without execute permission → **Permission denied**

### Key Learning

I learned how to create, read, execute files and manage Linux file permissions using `chmod`.
