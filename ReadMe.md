# 🔍 Root-Me Forensics – Deleted File
## 📌 Challenge Information
| Challenge Name - Deleted file 
| Category - Forensics
| Challenge Number-01 
| Operating System  - Kali Linux 
| Difficulty - Beginner 

## 🎯 Objective

A USB storage device was found containing digital evidence.
The objective was to recover a deleted file from the USB filesystem, analyze its metadata, and identify the owner of the device.
## 🛠️ Tools Used
- Kali Linux
- Sleuth Kit
- ExifTool
- Binwalk
- Linux Terminal
- SHA256sum
## 🔬 Investigation Process
### 1. Download the Challenge File
Downloaded the forensic evidence from Root-Me.

### 2. Extract the Evidence

gzip -dk ch39.gz
Identify the extracted file:
```bash
file ch39
```
### 3. Verify Evidence Integrity

```bash
sha256sum ch39
```
This generates a SHA-256 hash to help verify the evidence file's integrity.
### 4. Identify Deleted Files

Used Sleuth Kit to examine deleted filesystem entries.
```bash
fls -r -d usb.image
```
The command recursively lists deleted filesystem entries.

Identified the deleted PNG file and noted its inode address.

### 5. Recover the Deleted File

Used `icat` to recover the file using its inode address.

```bash
icat usb.image 5 > anonyme.png
```
*Note: Replace 5 with the actual inode address identified during the investigation.*

### 6. Verify the Recovered File

```bash
file anonyme.png
```
The recovered file was identified as a PNG image.
### 7. Analyze Image Metadata
Used ExifTool to inspect the metadata.
```bash
exiftool anonyme.png
```
Important metadata discovered:
```text
Creator: Javier Turcot
Image Size: 400x300
```
## 🧠 Findings
The deleted PNG image was successfully recovered from the USB filesystem.
Metadata analysis revealed the Creator field, which contained the name:
**Javier Turcot**
The challenge required the owner's name in lowercase, separated by an underscore.

## 🏁 Final Answer
```text
javier_turcot
```
## 📚 Key Learnings
1. Understanding digital forensic investigation.
2. Identifying deleted filesystem entries.
3. Using Sleuth Kit for filesystem analysis.
4. Recovering deleted files using inode addresses.
5. Extracting image metadata using ExifTool.
6. Understanding evidence integrity verification.

## 📝 Conclusion

This challenge demonstrated that deleting a file does not necessarily mean its data is permanently destroyed.

Using filesystem analysis and metadata extraction techniques, it was possible to recover a deleted image and identify information about the USB device's owner.

---

**Author:** Mr-incognito1202  
**Platform:** Root-Me  
**Domain:** Digital Forensics  
**Challenge:** Deleted File