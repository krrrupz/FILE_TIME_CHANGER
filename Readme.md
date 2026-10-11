<div align="center">

# 🕒 Windows File Timestamp Tool

### Update creation, last-modified, and last-access timestamps for files and folders with Python and PowerShell.

<p>
  <img src="https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Platform-Windows-0078D4?style=for-the-badge&logo=windows&logoColor=white" alt="Windows">
  <img src="https://img.shields.io/badge/Dependencies-None-2EA44F?style=for-the-badge" alt="No third-party dependencies">
  <img src="https://img.shields.io/badge/PowerShell-Required-5391FE?style=for-the-badge&logo=powershell&logoColor=white" alt="PowerShell">
</p>

<p>
  <a href="#-overview"><img src="https://img.shields.io/badge/Overview-5865F2?style=for-the-badge" alt="Overview"></a>
  <a href="#-features"><img src="https://img.shields.io/badge/Features-2EA44F?style=for-the-badge" alt="Features"></a>
  <a href="#-usage"><img src="https://img.shields.io/badge/Usage-orange?style=for-the-badge" alt="Usage"></a>
  <a href="#-warnings-and-limitations"><img src="https://img.shields.io/badge/Warnings-red?style=for-the-badge" alt="Warnings"></a>
</p>

</div>

---

## 📌 Overview

This small Python script asks for a folder path and a date/time, then runs a PowerShell command to set the timestamps of files and directories under that folder.

It uses Python's built-in `subprocess` module to invoke PowerShell, and PowerShell's .NET file-system methods to update timestamps.

> **Use responsibly:** File timestamps can be important for backups, synchronization, auditing, and investigations. Only change timestamps on files and folders you own or are authorized to manage. Changing timestamps does not change a file's contents.

## ✨ Features

- 📁 Prompts for a target folder path.
- 🗓️ Accepts a date and time in `DD/MM/YYYY HH:MM:SS` format.
- 🔁 Recursively enumerates items using `Get-ChildItem -Recurse -Force`.
- 📂 Updates creation, last-write, and last-access times for discovered files and directories.
- 🪟 Uses Windows PowerShell and .NET file-system APIs.
- 📦 Requires no third-party Python packages.

## 🛠️ Requirements

- Windows with PowerShell available.
- Python 3 installed and available from the command line.
- Permission to modify timestamps on the selected files and folders.

No `requirements.txt` dependencies are needed: `subprocess` is part of Python's standard library.

## 🚀 Usage

### 1. Save the script

Save the code in a file, for example:

```text
timestamp_tool.py
```

### 2. Open a terminal

Open Command Prompt or PowerShell and navigate to the directory containing the script.

### 3. Run it

```powershell
python timestamp_tool.py
```

### 4. Enter the requested values

Example inputs:

```text
Enter the folder path --> C:\Example\Project
Enter the date and time DD/MM/YYYY HH:MM:SS --> 15/08/2024 12:30:00
```

Use a valid folder path and a valid date/time. Test with a temporary folder first.

## 🕓 Which timestamps are changed?

For each item the script processes, it attempts to set:

| Timestamp | Meaning |
|---|---|
| Creation time | When the file or directory was created, as recorded by the file system. |
| Last-write time | When the file or directory was last modified, as recorded by the file system. |
| Last-access time | When the file or directory was last accessed, subject to Windows and file-system behavior. |

The script applies the same supplied time to each processed item.

## ⚠️ Warnings and limitations

- **Review the PowerShell command before running it.** The script modifies file-system metadata recursively.
- **The supplied snippet needs correction before it will work as intended.** The PowerShell block contains `"{set_time}"` and `f"{folder_path} ...`, but those are not Python f-strings inside the PowerShell script. Also, `.format(set_time)` supplies only one positional argument even though the string contains two named placeholders. Pass both values safely into the PowerShell command or build the script with correctly escaped/interpolated values.
- **Date parsing is locale-sensitive.** `Get-Date` may interpret `DD/MM/YYYY` differently depending on system settings. Use an explicit format and parse it deliberately to avoid ambiguous dates.
- **Hidden and system items may be included** because the command uses `-Force`.
- **The command targets descendants.** `Get-ChildItem` does not normally include the root folder itself in its results, so the root folder's timestamps may not be changed.
- **Access may be denied.** Protected files, folders, or files on restricted drives may fail to update.
- **Timestamp behavior varies** by file system, permissions, synchronization tools, and system settings.
- `-ExecutionPolicy Bypass` applies to the launched PowerShell process; use it only if you understand the implications and are authorized to run the script.

## 🔒 Safer-use checklist

- [ ] Test on a disposable folder first.
- [ ] Double-check the target path before confirming the operation.
- [ ] Use a date/time you can unambiguously identify.
- [ ] Avoid system folders and other people's data.
- [ ] Keep a record of the original timestamps if you may need to restore them.

## 📚 Built-in tools used

- Python [`subprocess`](https://docs.python.org/3/library/subprocess.html)
- Microsoft [PowerShell documentation](https://learn.microsoft.com/powershell/)
- .NET [`System.IO.File`](https://learn.microsoft.com/dotnet/api/system.io.file) and [`System.IO.Directory`](https://learn.microsoft.com/dotnet/api/system.io.directory)

---

<div align="center">

**Small script · No third-party Python packages · Windows-focused**

</div>
