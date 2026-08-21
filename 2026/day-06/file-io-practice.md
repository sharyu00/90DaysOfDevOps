# 🚀 Day 06 – Linux File Input & Output

## 📌 Objective

Practice creating, writing, appending, and reading text files using basic Linux commands.

### 1. Create a File

```bash
touch notes.txt
```

Creates an empty file.

### 2. Write to a File

```bash
echo "Line 1" > notes.txt
```

Writes content and **overwrites** existing data.

### 3. Append to a File

```bash
echo "Line 2" >> notes.txt
```

Adds content without deleting existing data.

### 4. Append with `tee`

```bash
echo "Line 3" | tee -a notes.txt
```

Shows the output on the terminal and appends it to the file.

### 5. Read the File

```bash
cat notes.txt
```

Displays the complete file.

### 6. Read First Lines

```bash
head -n 2 notes.txt
```

Displays the first 2 lines.

### 7. Read Last Lines

```bash
tail -n 2 notes.txt
```

Displays the last 2 lines.

## ✅ Quick Reference

| Command  | Use               |
| -------- | ----------------- |
| `touch`  | Create a file     |
| `>`      | Write / overwrite |
| `>>`     | Append            |
| `tee -a` | Display + append  |
| `cat`    | Read entire file  |
| `head`   | Read beginning    |
| `tail`   | Read end          |

## 🎯 Key Learning

Linux provides simple commands to create, modify, and inspect text files, which are commonly used in everyday system administration and DevOps tasks.
