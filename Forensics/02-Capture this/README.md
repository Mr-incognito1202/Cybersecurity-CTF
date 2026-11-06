# 🔍 Root-Me Forensics – Capture this
## 1. Challenge Information

 Platform - Root-Me 
 Challenge - Capture this
 Category - Forensics 
 Challenge Number - 02 
 Difficulty - 15 points 
 Operating System - Kali Linux 
## 2. Objective
The objective of this challenge was to investigate a PNG screenshot affected by the Acropalypse vulnerability.
The vulnerability can leave previously cropped image data in a PNG file, potentially exposing information that was intended to be removed.
The goal was to reconstruct the original screenshot, discover the KeePass database master password, and retrieve the final challenge answer.

## 3. Tools Used
- Kali Linux
- Python 3
- Acropalypse Restoration and Detection Multi-Tool
- ImageMagick
- ExifTool
- KeePassXC
- Git
## 4. Investigation Process
### Step 1: Identify the Challenge Files
The challenge evidence included:

- `capture.png` – PNG screenshot requiring forensic investigation.
- `database.kdbx` – Encrypted KeePass password database.
Commands:
```bash
cd ~/Downloads
ls -lh
file capture.png
file database.kdbx
```
### Step 2: Examine Image Metadata
Used ExifTool to inspect the PNG metadata.
```bash
exiftool capture.png
```
Also checked the image dimensions:
```bash
identify capture.png
```
### Step 3: Install ImageMagick
```bash
sudo apt update
sudo apt install imagemagick
```
ImageMagick was used to inspect the image properties and dimensions.
### Step 4: Download the Acropalypse Recovery Tool
Cloned the recovery repository:
```bash
git clone https://github.com/frankthetank-music/Acropalypse-Multi-Tool.git
```
Navigated into the repository:
```bash
cd Acropalypse-Multi-Tool
```
### Step 5: Install Dependencies
Created a Python virtual environment:
```bash
python3 -m venv venv
source venv/bin/activate
```
Installed the required libraries:
```bash
pip install Pillow==9.5.0 sv_ttk==2.4.3
```
### Step 6: Launch the Recovery Application
```bash
python gui.py
```
The Acropalypse application provides two main features:

- DetectTool – Detects potentially vulnerable images.
- RestoreTool – Attempts to reconstruct previously cropped image data.

### Step 7: Restore the Screenshot
The restoration procedure:

1. Opened RestoreTool.
2. Selected `capture.png`.
3. Selected the appropriate screenshot-source preset.
4. Started the restoration process.
5. Saved the reconstructed image as `restored.png`.

**Important:** The correct preset and original image dimensions are required for successful reconstruction.
### Step 8: Analyze the Reconstructed Image
Opened the recovered screenshot and inspected its contents for information that could reveal the KeePass master password.
The recovered information was then used to access the encrypted database.

### Step 9: Access the KeePass Database
Opened the database:
```bash
keepassxc database.kdbx
```
Entered the recovered master password to unlock the database.
Inspected its stored entries to identify the challenge validation answer.
## 5. Vulnerability Explained
**Acropalypse – CVE-2023-21036**
Acropalypse is a vulnerability affecting certain screenshot editing workflows.
When an image is cropped and saved, the application may fail to properly remove the original image data.

As a result, information hidden outside the visible cropped region may remain recoverable.

This can expose sensitive information that users believed had been permanently removed.

## 6. Final Answer
**Root-Me validation flag:**
```text
@cropalypse_vuln_is_impressive
```
## 7. Skills Learned
- Digital image forensics.
- PNG file structure analysis.
- Understanding the Acropalypse vulnerability.
- Recovering cropped image information.
- Python virtual environment management.
- Using forensic recovery tools.
- KeePass database investigation.
- Password database analysis.

## 8. Conclusion

This challenge demonstrated how image editing vulnerabilities can expose sensitive information even after users believe it has been removed.

By investigating the PNG screenshot and reconstructing previously cropped image data, information needed to unlock an encrypted KeePass database could be recovered.

The challenge highlights the importance of secure image sanitization and proper handling of digital evidence.

---

**Author:** Mr-incognito1202  
**Platform:** Root-Me  
**Domain:** Digital Forensics  
**Challenge:** Capture this