# ZAL11 Modified - Enhanced SAP File Manager

A customized, dynpro-free version of the SAP AL11 File Management transaction with a modern dual-pane GUI interface.

![SAP ABAP](https://img.shields.io/badge/SAP-ABAP-blue)
![Version](https://img.shields.io/badge/version-1.0-green)
![License](https://img.shields.io/badge/license-MIT-yellow)

## 📖 Overview

This is a customization specifically designed for the SAP File Management System. It provides a graphical interface for navigating, managing, and transferring files between local PCs and SAP application servers, without requiring traditional dynpro screens.

### Key Enhancements from Original ZAL11

- ✅ **Dynpro-Free Architecture** - Uses `CL_GUI_DOCKING_CONTAINER` instead of custom containers
- ✅ **Dialog-Based CHMOD** - Replaced screen 200 with `CL_GUI_DIALOGBOX_CONTAINER`
- ✅ **Preserved Functionality** - All original features maintained
- ✅ **Cross-Platform Support** - Works with Windows and Unix/Linux servers

## 🎯 Features

### File Navigation
- 🗂️ Dual-pane interface (Local PC + SAP Server)
- 🌳 Expandable folder tree navigation
- 📊 ALV Grid file listings with sorting/filtering
- 🔍 50+ file type recognition with icons

### File Operations
- ⬆️ Upload files to server
- ⬇️ Download files to local PC
- 📁 Create, rename, copy, move folders
- 🗑️ Delete files and folders
- 🖱️ Drag & drop support

### Advanced Features
- 📦 Compress files (TAR+BZ2 on Unix, ZIP on Windows)
- 📂 Uncompress archives (ZIP, TAR, GZ, BZ2)
- 🔐 CHMOD permissions (Unix) / ATTRIB (Windows)
- ⭐ Server shortcuts/bookmarks
- 📋 Copy path to clipboard
- 🔗 Open files with default application

## 📁 Project Structure

```
zal11_modified/
├── ZAPP_SERVER    # Main program entry point
├── ZAPP_TOP       # Global data declarations & types
├── ZAPP_CLS       # Class definitions & implementations
└── ZAPP_SUB       # Subroutines & business logic
```

### File Descriptions

| File | Size | Description |
|------|------|-------------|
| `ZAPP_SERVER` | ~5 KB | Main report with includes and START-OF-SELECTION |
| `ZAPP_TOP` | ~16 KB | Data types, global variables, constants, GUI objects |
| `ZAPP_CLS` | ~50 KB | OO classes for server operations and event handling |
| `ZAPP_SUB` | ~120 KB | FORM routines for UI initialization and file operations |

## 🏗️ Architecture

### Class Hierarchy

```
lif_server_command (Interface)
├── lcl_aix_server      # Unix/Linux implementation
└── lcl_windows_server  # Windows implementation

lcl_application         # GUI event handler class
```

### GUI Components

```
CL_GUI_DOCKING_CONTAINER
└── CL_GUI_SPLITTER_CONTAINER (2 rows)
    ├── Row 1: Local PC Panel
    │   ├── CL_GUI_SIMPLE_TREE (folder tree)
    │   └── CL_GUI_ALV_GRID (file listing)
    └── Row 2: SAP Server Panel
        ├── CL_GUI_SIMPLE_TREE (folder tree)
        └── CL_GUI_ALV_GRID (file listing)
```

## 🚀 Installation

### Prerequisites
- SAP NetWeaver 7.0 or higher
- SAP GUI for Windows
- Appropriate authorizations for file operations

### Steps

1. Create a new program in SE38/SE80
2. Copy `ZAPP_SERVER` content as the main program
3. Create includes:
   - `ZAPP_TOP`
   - `ZAPP_CLS`
   - `ZAPP_SUB`
4. Activate all objects
5. Execute the program

## ⚙️ Configuration

### Customization Options (in `ZAPP_TOP`)

```abap
DATA : BEGIN OF s_customize,
         root_path(600)  TYPE c VALUE '',      " Default server root path
         root_name(20)   TYPE c VALUE '',      " Display name for root
         autodirsize(1)  TYPE c VALUE space,   " Auto calculate folder sizes
         logical_path(1) TYPE c VALUE abap_true,
         total_on_top(1) TYPE c VALUE abap_true,
         confirm_dl(1)   TYPE c VALUE abap_true, " Confirm downloads
         auth_object(20) TYPE c VALUE '',      " Authorization object
         auth_id(10)     TYPE c VALUE '',      " Authorization ID
       END OF s_customize.
```

### Authorization Flags

All operations can be individually controlled:

| Flag | Operation |
|------|-----------|
| `download` | Download files |
| `upload` | Upload files |
| `overwrite` | Overwrite existing files |
| `zip/unzip` | Compression operations |
| `rename_file/folder` | Rename operations |
| `delete_file/folder` | Delete operations |
| `create_folder` | Create new folders |
| `chmod` | Change permissions |
| `move_file/folder` | Move operations |

## 📝 Usage

1. **Run the program** - Execute `ZAPP_SERVER`
2. **Navigate folders** - Click on tree nodes to expand
3. **View files** - File details shown in ALV grid
4. **Transfer files** - Drag & drop or use context menu
5. **Manage files** - Right-click for operations menu

### Keyboard Shortcuts

- Double-click folder: Navigate into
- Double-click file: Open with default app
- Right-click: Context menu with operations

## 🔗 Credits

### Original Code
- **Program**: ZAL11 (Custom AL11)
- **Author**: S. Hermann
- **Website**: http://quelquepart.biz
- **Version**: 2.4.3
- **Date**: November 28, 2016

### Modifications
- **Author**: Sunil Singh Bora
- **Contact**: sunilbora@microsoft.com
- **Date**: January 2026
- **Changes**: Dynpro removal, docking container implementation

## 📄 License

This project is provided as-is for educational and internal use purposes.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📧 Support

For questions or issues, contact: sunilbora@microsoft.com
