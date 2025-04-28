import os
import shutil
import datetime
import sys

# Defining function to move specific type of files from one folder to another
def move_files_by_extension(source_folder, destination_folder, file_ext):
    # Automatically add dot if not present
    if not file_ext.startswith("."):
        file_ext = "." + file_ext
    
    files_copied = False
    # Loop through the files and move the ones with the selected extension
    try:
        for file_name in os.listdir(source_folder):
            file_path = os.path.join(source_folder, file_name)

            if os.path.isfile(file_path) and file_name.endswith(file_ext):
                if os.path.exists(dest_path):
                    print(f"File '{file_name}' already exists in the destination folder.")
                    choice = input("Do you want to [O]verwrite, [R]ename, or [S]kip this file? ").strip().lower()

                    if choice == 's':
                        print(f"Skipped: {file_name}")
                        continue
                    elif choice == 'r':
                        base, ext = os.path.splitext(file_name)
                        new_name = input(f"Enter a new name for '{file_name}' (without extension): ").strip()
                        new_file_name = f"{new_name}{ext}"
                        dest_path = os.path.join(destination_folder, new_file_name)

                
                # shutil.copy2(file_path, os.path.join(destination_folder, file_name))
                try:
                    shutil.copy2(file_path, os.path.join(destination_folder, file_name))
                    print(f"Copied: {file_name}")
                    files_copied = True
                except Exception as e:
                    print(f"Failed to copy {file_name}: {e}")
    except Exception as e:
        print(f"Error accessing files: {e}")
        return

    
    if not files_copied:
        print(f"There are no files with the extension '{file_ext}' in the source folder.")
    else:
        print(f"All '{file_ext}' files have been copied to: {destination_folder}")


# Defining function to move files from one folder to another based on file size
def copy_files_based_on_size(source_folder, destination_folder, max_size, unit='MB'):
    if max_size <= 0:
        print("Error: max_size must be a positive number.")
    unit = unit.upper()
    if unit not in ['MB', 'KB']:
        print("Error: Invalid unit. Please enter 'MB' or 'KB'.")
    
    # Convert size to KB
    if unit == 'MB':
        max_size_kb = max_size * 1024 * 1024
    elif unit == 'KB':
        max_size_kb = max_size * 1024
    else:
        print("Invalid unit. Please enter 'MB' or 'KB'.")
        return

    files_copied = False

    for file in os.listdir(source_folder):
        path = os.path.join(source_folder, file)

        if os.path.isfile(path) and os.path.getsize(path) <= max_size_kb:
            if os.path.exists(dest_path):
                choice = input(f"File '{file}' already exists. Do you want to overwrite (y/n)? ").strip().lower()
                if choice == 'y':
                    shutil.copy2(path, dest_path)
                    print(f"Overwritten: {file}")
                else:
                     print(f"Skipped: {file}")
            else:                            
                try:
                    shutil.copy2(path, os.path.join(destination_folder, file))
                    print(f"Copied: {file}")
                    files_copied = True
                except PermissionError:
                    print(f"Permission denied: {file}")
                except OSError as e:
                    print(f"Error copying file {file}: {e}")               

    if not files_copied:
        print(f"No files smaller than or equal to {max_size}{unit} found in source folder.")


def copy_recent_modified_files(source_folder, destination_folder, days):
    today = datetime.date.today()
    from_date = today - datetime.timedelta(days=days)
    from_time = datetime.datetime.combine(from_date, datetime.time.min)

    files_copied = False

    for file in os.listdir(source_folder):
        file_path = os.path.join(source_folder, file)

        if os.path.isfile(file_path):
            modified_time = datetime.datetime.fromtimestamp(os.path.getmtime(file_path))

            if modified_time >= from_time:
                try:
                    shutil.copy2(file_path, destination_folder)
                    print(f"Copied: {file}")
                    files_copied = True
                except Exception as e:
                    print(f"Failed to copy {file}: {e}")

    if not files_copied:
        print(f"No files modified since {from_time.strftime('%Y-%m-%d %H:%M:%S')}.")

# Ask the user for the operation they want to perform
print("Choose the operation:")
print("1. Move files by extension")
print("2. Copy small files based on size")
print("3. Copy recent files based on last modified date")

choice = input("Enter 1, 2, or 3: ").strip()

# Prompt the user for the source and destination folder paths
source = input("Enter source folder path: ").strip()
if not os.path.isdir(source):
    print(f"Error: Source folder '{source}' does not exist or is not a directory.")
    sys.exit(1)
if len(os.listdir(source)) == 0:
    print(f"Warning: Source folder '{source}' is empty.")
    sys.exit(1)

    
destination = input("Enter destination folder path: ").strip()
if not os.path.isdir(destination):
    try:
        os.makedirs(destination, exist_ok=True)
    except Exception as e:
        print(f"Error creating destination folder: {e}")


# Call the appropriate function based on user's choice
if choice == '1':
    file_ext = input("Enter the file extension to move (e.g., .csv, .json): ").strip()
    move_files_by_extension(source, destination, file_ext)

elif choice == '2':
    max_size = float(input("Enter the max file size (in MB or KB): ").strip())
    unit = input("Enter the unit (MB or KB): ").strip()
    copy_files_based_on_size(source, destination, max_size, unit)

elif choice == '3':
    days = int(input("Enter the number of days back (e.g., 0 for today, 1 for yesterday): ").strip())
    copy_recent_modified_files(source, destination, days)

else:
    print("Invalid choice! Please select 1, 2, or 3.")
