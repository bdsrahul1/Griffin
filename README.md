# 🛡️ GRIFFIN File Analyzer

<div align="center">
  <img src="https://raw.githubusercontent.com/bdsrahul1/Griffin/main/griffin_1.jpg" alt="GRIFFIN File Analyzer" width="800">
</div>

**Guardian of File Integrity & Type Analysis**

A powerful malware research and forensics tool for comprehensive file type detection, hash calculation, and intelligent file organization. Built for security analysts, incident responders, and malware researchers.

![License](https://img.shields.io/badge/License-MIT-green.svg)
![Platform](https://img.shields.io/badge/Platform-Windows-blue.svg)

---

## ✨ Features

### 🔍 **File Type Detection**
- **140+ File Types Supported**: Executables, Office documents, scripts, images, archives, databases, and more
- **Binary Signature Detection**: Strong detection for PE/ELF/Mach-O executables, DLLs, and DMG files
- **Multi-Layer Detection**: Binary headers → Magic library → Content analysis → Extension mapping → MIME types
- **Script Type Detection**: Python, PowerShell, Bash, JavaScript, VBScript, Batch, Perl, Ruby, PHP, and more
- **Macro-Enabled Office Files**: Detects .docm, .xlsm, .pptm, .dotm formats

### 🔐 **File Hashing**
- **SHA256 Hash Calculation**: Memory-efficient 4KB chunk processing for large files
- **Duplicate Detection**: Identify identical files by hash comparison
- **Audit Trail**: Complete hash logging for forensic investigations

### 📊 **File Organization**
- **Intelligent Auto-Sort**: Organize files into type-based folder structure
- **Two Modes**: Move (fast) or Copy (safe, preserves originals)
- **Structure Preservation**: Maintains original directory hierarchy or flatten option
- **Duplicate Handling**: Automatic filename conflict resolution with numerical suffixes
- **Path Safety**: Windows MAX_PATH compliance with 100-character truncation
- **Confirmation Prompts**: Review before executing file operations (bypass with `--no-confirm`)

### 📈 **Reporting & Output**
- **Excel Reports**: Multi-sheet workbooks with analysis, summary, and metadata
- **Speed Mode**: Progress bar with percentage and file count for large datasets
- **Operation Logging**: Complete audit trail of all file movements/copies
- **File Type Statistics**: Distribution analysis of analyzed files

---

## 🚀 Quick Start

```bash
# Download GRIFFIN_FileAnalyzer.exe
# No installation required - works on any Windows machine

GRIFFIN_FileAnalyzer.exe C:\path\to\analyze
```

---

## 📦 Installation

1. Download `GRIFFIN_FileAnalyzer.exe` from [Releases](../../releases)
2. Run directly - no Python installation needed
3. Size: ~50 MB (all dependencies bundled)

**That's it!** No dependencies, no setup, just download and run.

---

## 💡 Usage Examples

### 1️⃣ Basic Analysis (Read-Only)
Generate Excel report with file types and SHA256 hashes.
```bash
GRIFFIN_FileAnalyzer.exe C:\Samples
```
**Output:** `file_analysis_20260128_205623.xlsx`

### 2️⃣ Custom Output Location
```bash
GRIFFIN_FileAnalyzer.exe C:\Samples --output C:\Reports\malware_analysis.xlsx
```

### 3️⃣ Organize Files (Move Mode - Fast)
Sort files into type-based folders after analysis.
```bash
GRIFFIN_FileAnalyzer.exe C:\Samples --organize
```
**Result:**
```
C:\Samples_organized\
  ├── EXE_Files\
  ├── DLL_Files\
  ├── PDF_Documents\
  ├── ZIP_Archives\
  └── ...
```

### 4️⃣ Organize with Copy (Safe Mode)
Preserve original files while creating organized copies.
```bash
GRIFFIN_FileAnalyzer.exe C:\Samples --organize --mode copy
```

### 5️⃣ Custom Organization Directory
```bash
GRIFFIN_FileAnalyzer.exe C:\Samples --organize --organize-dir C:\Sorted
```

### 6️⃣ Flatten Directory Structure
Remove subdirectories and place all files directly in type folders.
```bash
GRIFFIN_FileAnalyzer.exe C:\Samples --organize --flatten
```

### 7️⃣ Speed Mode (Large Datasets)
Minimal output with progress bar for processing thousands of files.
```bash
GRIFFIN_FileAnalyzer.exe C:\Samples --organize --speed
```
**Output:**
```
Progress: [▓▓▓▓▓▓▓▓▒▒] 82.5% | 3,245/3,932 files
```

### 8️⃣ Automated Processing (No Confirmation)
```bash
GRIFFIN_FileAnalyzer.exe C:\Samples --organize --no-confirm --speed
```
⚠️ **Caution:** Skips confirmation prompts - use for scripting/automation only!

---

## 🎮 Command-Line Arguments

| Argument | Type | Description |
|----------|------|-------------|
| `folder` | Required | Path to folder to analyze |
| `--output`, `-o` | Optional | Custom Excel report path (default: `file_analysis_YYYYMMDD_HHMMSS.xlsx`) |
| `--organize` | Flag | Enable file organization into type-based folders |
| `--mode` | Choice | Organization mode: `move` (fast) or `copy` (safe). Default: `move` |
| `--organize-dir` | Optional | Custom directory for organized files (default: `{folder}_organized`) |
| `--no-confirm` | Flag | Skip confirmation prompt - proceed automatically |
| `--flatten` | Flag | Ignore subdirectories, place all files directly in type folders |
| `--speed` | Flag | Show progress bar, reduce console output for faster processing |

---

## 📋 Supported File Types

### 🖥️ **Executables & Binaries**
Windows PE (EXE, DLL, SYS), Linux ELF, macOS Mach-O/DMG, Java JAR/CLASS, Python PYC

### 📄 **Documents**
PDF, Word (DOC/DOCX/DOCM), Excel (XLS/XLSX/XLSM), PowerPoint (PPT/PPTX/PPTM), RTF, ODT/ODS/ODP

### 📜 **Scripts**
Python, PowerShell (PS1/PSM1), Bash/Shell, JavaScript, VBScript, Batch, Perl, Ruby, PHP

### 🗜️ **Archives**
ZIP, RAR, 7Z, TAR, GZ, BZ2, XZ, ISO, CAB

### 🖼️ **Images**
PNG, JPG, GIF, BMP, ICO, SVG, TIFF, WebP

### 🎥 **Media**
MP4, AVI, MKV, MOV, MP3, WAV, FLAC

### 🗄️ **Databases**
SQLite, MySQL, PostgreSQL, Access (MDB), CSV

### ⚙️ **Configuration**
JSON, XML, YAML, INI, TOML, CONFIG, CONF

---

## 📊 Excel Report Structure

### Sheet 1: File_Analysis
| Column | Description |
|--------|-------------|
| Filename | Original filename |
| File_Path | Full file path |
| File_Type | Detected file type |
| SHA256_Hash | Cryptographic hash |

### Sheet 2: Summary
- Total files analyzed
- File type distribution
- Top 10 most common types

### Sheet 3: Metadata
- Analysis timestamp
- Tool version
- Arguments used
- Processing statistics

---

## 🛠️ Advanced Features

### Binary Signature Detection
Reads first 4096 bytes to identify executables before magic library:
- **PE Executables**: `MZ` header → DOS stub → PE signature
- **ELF Binaries**: `\x7fELF` magic bytes
- **Mach-O**: `0xFEEDFACE`, `0xFEEDFACF`, `0xCAFEBABE`
- **DMG Images**: `koly` signature at EOF-512 bytes

### Duplicate File Handling
Automatically resolves filename conflicts:
```
malware.exe       → EXE_Files\malware.exe
malware.exe (dup) → EXE_Files\malware_1.exe
malware.exe (dup) → EXE_Files\malware_2.exe
```

### Path Length Protection
Prevents Windows MAX_PATH errors by truncating folder names to 100 characters.

---

## 🎨 User Interface

### Banner 
```
╔══════════════════════════════════════════════════════════════════════════╗
║                                                                          ║
║ ═══════════════════════════════════════════════════════════════════════ ║
║                                                                          ║
║   ██████╗ ██████╗ ██╗███████╗███████╗██╗███╗   ██╗                     ║
║  ██╔════╝ ██╔══██╗██║██╔════╝██╔════╝██║████╗  ██║                     ║
║  ██║  ███╗██████╔╝██║█████╗  █████╗  ██║██╔██╗ ██║                     ║
║  ██║   ██║██╔══██╗██║██╔══╝  ██╔══╝  ██║██║╚██╗██║                     ║
║  ╚██████╔╝██║  ██║██║██║     ██║     ██║██║ ╚████║                     ║
║   ╚═════╝ ╚═╝  ╚═╝╚═╝╚═╝     ╚═╝     ╚═╝╚═╝  ╚═══╝                     ║
║                                                                          ║
║          [ Guardian of File Integrity & Type Analysis ]                 ║
║                                                                          ║
║          ▸ File Type Detection  ▸ Hashing  ▸ File Organizing            ║
║                                                                          ║
║ ═══════════════════════════════════════════════════════════════════════ ║
║                                                   ══Author: Rahul        ║
╚══════════════════════════════════════════════════════════════════════════╝
```

### Progress Bar (Speed Mode)
```
Progress: [▓▓▓▓▓▓▓▓▒▒] 82.5% | 3,245/3,932 files
```

---

## 🔒 Safety Features

✅ **Confirmation Prompts**: Review file operations before execution  
✅ **Operation Logging**: Complete audit trail saved to `organization_log.txt`  
✅ **Duplicate Protection**: Prevents overwriting with automatic renaming  
✅ **Path Validation**: Ensures Windows MAX_PATH compliance  
✅ **Error Handling**: Graceful failure with detailed error messages  
✅ **Read-Only Mode**: Default analysis doesn't modify files  

---

## 🐛 Troubleshooting

### Issue: "Failed to execute script" on EXE
**Solution:** Download the latest release build (already fixed)

### Issue: "Permission Denied" errors
**Solution:** Run as Administrator (Windows)

### Issue: Unicode errors in Windows CMD
**Solution:** Run `chcp 65001` before executing, or use PowerShell instead

---

## 📝 License

MIT License - See [LICENSE](LICENSE) file for details

---

## 👤 Author

**Rahul**

---

## 🤝 Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## ⭐ Acknowledgments

- Built with python-magic for file type detection
- pandas for data processing
- openpyxl for Excel report generation
- PyInstaller for standalone executable packaging

---

## 📞 Support

For bug reports and feature requests, please open an [Issue](../../issues).

---

<div align="center">

**🛡️ GRIFFIN - Guardian of File Integrity & Type Analysis 🛡️**

*Empowering security professionals with intelligent file analysis and organization*

</div>
