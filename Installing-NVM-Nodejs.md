## Next.js Development Setup Guide (Node.js & nvm)
This document guides you through installing Node.js via Node Version Manager (nvm) and troubleshooting Windows PowerShell permission issues.
------------------------------
## 1. Why Use nvm Instead of Direct Installation?

* Avoid permission errors: Direct Node.js installers often cause global package installation failures (EACCES).
* Easy switching: Switch between multiple Node.js versions with a single command.
* Seamless updates: Update to the newest Node.js version instantly without uninstalling previous versions.

------------------------------
## 2. Installation Guide## 🪟 Windows (Using nvm-windows)

   1. Download: Visit the nvm-windows releases page on GitHub.
   2. Install: Download and run the nvm-setup.exe installer.
   3. Open Terminal: Open a new PowerShell or Command Prompt window.
   4. Install Node.js: Run the following command to get the latest stable Long-Term Support (LTS) version:
   
   nvm install lts
   
   5. Activate Node.js: Enable the installed version by running:
   
   nvm use lts
   
   
## 🍏 Mac / 🐧 Linux (Using nvm)

   1. Install script: Open your terminal and run:
   
   curl -o- githubusercontent.com | bash
   
   2. Refresh terminal: Close and reopen your terminal, or run:
   
   source ~/.bashrc
   
   3. Install Node.js: Download the latest stable version:
   
   nvm install --lts
   
   4. Activate Node.js: Run:
   
   nvm use --lts
   
   
------------------------------
## 3. Verification
Confirm your installation by checking the version numbers:

node -v
npm -v

------------------------------
## 4. Troubleshooting: Windows Script Execution Error## The Problem
When running npm -v, you may encounter the following security error in PowerShell:

npm : File C:\nvm4w\nodejs\npm.ps1 cannot be loaded because running scripts is disabled on this system.

This occurs because Windows disables third-party script execution by default.
## The Solution

   1. Open the Windows Start Menu.
   2. Search for PowerShell.
   3. Right-click it and select Run as Administrator.
   4. Execute the following command to allow local scripts to run:
   
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   
   5. Type Y (or A) and press Enter to confirm the change.
   6. Close the Administrator window, open a new standard PowerShell window, and re-test npm -v.

