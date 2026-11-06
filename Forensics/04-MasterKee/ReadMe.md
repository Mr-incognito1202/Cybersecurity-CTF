# Root-Me – MasterKee

## Challenge Information
 Platform | Root-Me |
 Category | Forensics |
 Challenge | MasterKee |
 Points | 15 |
 Difficulty | Intermediate |
 Vulnerability - CVE-2023-32784 
 Tool | KeePass / KeePassXC, keepass2john, John the Ripper |

## 1. Challenge Description
A colleague has installed a useful password-management system on a new machine. He claims that he is the only person who can access it because only he knows the master password.
The objective is to investigate the provided evidence, analyze the KeePass password database, and recover the master password.
## 2. Tools Used
- Kali Linux
- KeePass / KeePassXC
- John the Ripper
- keepass2john
- Python 3
## 3. Understanding the Vulnerability
The challenge is associated with **CVE-2023-32784**, a vulnerability affecting KeePass versions before 2.54.
The vulnerability can expose fragments of a master password through memory remnants left behind during password entry.
These remains can potentially be recovered from a memory dump and analyzed to reconstruct the original password.
## 4. Investigation Methodology
### Step 1: Identify the Provided Files
List the extracted challenge files:
```bash
ls -lah
file *
```
Identify the KeePass database and any memory dump or supporting evidence.
### Step 2: Analyze the KeePass Database
Inspect the database file:
```bash
file database.kdbx
```
`.kdbx` file is a KeePass password database.

### Step 3: Investigate Password Memory Artifacts
Analyze the provided memory evidence for remnants associated with KeePass master-password entry.
The objective is to recover the password fragments and reconstruct the original master password.
### Step 4: Recover and Validate the Password
Use the recovered password fragments to reconstruct the master password, then test it against the provided KeePass database.
Only consider the password validated when KeePass successfully opens the database.
## 5. Results

- Identified the KeePass database.
- Investigated the password-related memory artifacts.
- Studied the impact of CVE-2023-32784.
- Reconstructed and validated the master password.

**Master password:** `REPLACE_WITH_YOUR_VALIDATED_PASSWORD`

**Root-Me flag:** `REPLACE_WITH_YOUR_ACTUAL_FLAG`

- Understanding KeePass password database files.
- Learning how memory artifacts can expose sensitive information.
- Understanding CVE-2023-32784.
- Practicing digital forensics and password recovery.
- Understanding why sensitive information should be cleared from memory securely.

Documented as part of my Root-Me cybersecurity and digital forensics practice.
Author Mr-incognito1202