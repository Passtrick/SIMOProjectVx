# VirtualXposed

## Overview

VirtualXposed is an Android application that enables running Xposed modules without requiring root access. It is built on top of VirtualApp (a virtual Android environment) and epic (an ART hook framework). The project supports Android versions 5.0 through 10.0.

The application works by creating a virtual Android environment where apps and Xposed modules can be installed and run in isolation from the main system. This allows users to use Xposed modules for app customization without modifying their device's system partition.

**Key Limitations:**
- Cannot modify system-level functionality (system apps, framework modifications)
- Resource hooks are not currently supported (affects theming modules)
- Commercial use is prohibited per VirtualApp's licensing terms

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Core Components

**Virtual Environment Layer (VirtualApp)**
- Problem: Running Xposed modules traditionally requires root access and system modification
- Solution: Uses VirtualApp to create an isolated virtual Android environment where apps run in a sandboxed container
- Approach: Apps installed in VirtualXposed run within this virtual environment, completely separate from the host system

**ART Hook Framework (epic)**
- Problem: Need to intercept and modify app behavior at runtime without root
- Solution: epic provides ART (Android Runtime) hooking capabilities that work in userspace
- Approach: Enables Xposed-style method hooking within the virtual environment without requiring system-level access

**Module Management (XposedInstaller)**
- Built-in XposedInstaller allows users to browse, install, and manage Xposed modules
- Modules are activated through the standard Xposed module interface
- Reboot functionality is virtual (only restarts the virtual environment, not the device)

### App Installation Methods

1. **Clone from system** - Copy apps already installed on the device into the virtual environment
2. **APK file installation** - Install directly from APK files on external storage
3. **File chooser installation** - Select APK files through Android's file picker

### Isolation Model

All apps and modules must be installed within VirtualXposed to function together. Installing an app in the real system and a module in VirtualXposed (or vice versa) will not work - both must exist in the same virtual environment.

## External Dependencies

### Core Frameworks
- **VirtualApp** - Virtual Android environment framework (non-commercial license)
- **epic** - ART hook library for Android runtime method interception

### Build & CI
- **Travis CI** - Continuous integration for automated builds

### Platform Requirements
- Android 5.0 (Lollipop) through Android 10.0
- No root access required
- Standard Android permissions for virtual environment operation

### Licensing Restrictions
- VirtualApp is not licensed for commercial use
- Contact original author (Lody - imlody@foxmail.com) for commercial licensing inquiries