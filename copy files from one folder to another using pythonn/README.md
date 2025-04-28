## 📚 Python Modules Used

| Module | Why It’s Used | Key Functions |
|:------|:--------------|:--------------|
| `os` | To interact with the operating system (like reading folders, checking if a file/folder exists). | `listdir()`, `path.join()`, `path.isfile()`, `path.isdir()`, `makedirs()` |
| `shutil` | To copy or move files and folders easily. | `copy2()`, `copy()`, `copytree()`, `move()`, `rmtree()` |
| `datetime` | To work with dates and times (for checking file modification dates). | `date.today()`, `datetime.timedelta`, `datetime.fromtimestamp()` |
| `sys` | To exit the script if necessary (error handling). | `sys.exit()` |

---

## 🛠️ Important Keywords Explained

### 1. `os`
- **What:** Built-in module to interact with the operating system.
- **Why:** 
  - Read files inside folders (`os.listdir()`).
  - Join folder and file paths safely (`os.path.join()`).
  - Check if something is a file (`os.path.isfile()`) or a folder (`os.path.isdir()`).
  - Create a folder if it doesn't exist (`os.makedirs()`).

---

### 2. `shutil`
- **What:** Shell utilities to copy, move, and delete files and folders.
- **Why:**
  - `shutil.copy2()`: Copy files along with metadata like modified date, permissions.
  - `shutil.copy()`: Copy files without metadata.
  - `shutil.copytree()`: Copy entire folders recursively.
  - `shutil.move()`: Move files or folders (deletes from the source).
  - `shutil.rmtree()`: Remove entire folders.

---

### 3. `datetime`
- **What:** Built-in module to handle dates and times.
- **Why:**
  - To calculate the cutoff date for "recently modified files."
  - `datetime.date.today()`: Gets today's date.
  - `datetime.timedelta(days=N)`: Subtracts N days from today.
  - `datetime.datetime.fromtimestamp()`: Converts file's modified timestamp into readable format.

---

### 4. `sys`
- **What:** System-specific functions and parameters.
- **Why:**
  - `sys.exit(1)`: Stops the program if a serious error is found (e.g., source folder doesn't exist or is empty).

---

### 5. `input()`
- **What:** Built-in Python function to **get user input** from the console.
- **Why:** 
  - Asking user which operation to perform (Move by extension / Copy by size / Copy by date).
  - Asking for file extensions, sizes, folder paths, overwrite or rename choices, etc.

---

### 6. `try-except`
- **What:** Python error-handling block.
- **Why:**
  - To catch and handle errors like permission denied, file not found, etc.
  - Ensures the script doesn't crash if it encounters a problematic file.

---

### 7. `if-else`
- **What:** Decision making in Python.
- **Why:**
  - Choosing operations based on user input (`if choice == '1'`, etc.).
  - Checking if a file or folder exists (`if os.path.exists()`).
  - Handling overwrite/rename/skip options for duplicate files.

---

### 8. `for` loop
- **What:** Repeating action for every item in a list.
- **Why:**
  - To process every file inside a folder one-by-one.

---

## 🚀 Functions Explained

| Function | Purpose |
|:---------|:--------|
| `move_files_by_extension()` | Copies files with a specific extension (e.g., .csv, .json) from source to destination. |
| `copy_files_based_on_size()` | Copies files smaller than or equal to a specified size (in MB/KB). |
| `copy_recent_modified_files()` | Copies files modified in the last N days. |

Each function takes `source_folder` and `destination_folder` as input parameters.

---

## 🧩 Flow of the Script

1. Ask user to select operation (by extension / by size / by date).
2. Ask user for source and destination folder paths.
3. Based on selection:
   - Call appropriate function.
   - Inside function, loop through files, check condition, and copy files.
4. Handle special cases like:
   - File already exists (Overwrite, Rename, Skip).
   - Permission errors.
   - Empty folders.
5. Print success or error messages.

---

## ⚡ Choices Handling

- `[O]verwrite` → Replace the existing file in the destination.
- `[R]ename` → Let user rename the file before copying.
- `[S]kip` → Skip copying this file.

---

## 📌 Notes

- The script does **NOT** delete the original files after copying.
- The script preserves file timestamps when copying.
- Empty source folders or invalid paths will cause the script to exit early.

---

# 📜 Example Run

```bash
Choose the operation:
1. Move files by extension
2. Copy small files based on size
3. Copy recent files based on last modified date
Enter 1, 2, or 3: 1
Enter source folder path: /home/user/documents
Enter destination folder path: /home/user/backup
Enter the file extension to move (e.g., .csv, .json): .csv
Copied: report.csv
Copied: sales.csv
All '.csv' files have been copied to: /home/user/backup
```

---

# ✅ Conclusion

This utility script is useful for file management tasks like backups, filtering files, organizing folders based on size or modification time — **without needing to manually sort files**.

---

