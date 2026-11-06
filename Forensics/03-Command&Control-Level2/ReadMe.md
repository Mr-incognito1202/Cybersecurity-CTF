# Root-Me – Command & Control-level2
## 1. Challenge Description
The challenge provides a Windows memory dump. The objective is to identify the workstation's hostname because it was not recorded during the investigation.
Instead of analyzing a live system, we perform **memory forensics** on the provided RAM dump to recover system information.
## 2. Tools Required
- Kali Linux
- Volatility 3 (or Volatility 2)
- Terminal
- `tar` for extracting the challenge archive
## 3. Download and Extract the Evidence
Download the challenge archive from Root-Me. The downloaded file is named `ch2.tbz2`.
Extract it:

```bash
tar -xvjf ch2.tbz2
```
The extracted memory dump should be:
```text
ch2.dmp
```
Navigate to the directory containing the dump:
```bash
cd /path/to/challenge/
``
## 4. Memory Analysis Using Volatility 3
Check that Volatility is available:
```bash
python3 vol.py -h
```
Identify basic Windows system information:
```bash
python3 vol.py -f ch2.dmp windows.info
```
List the registry hives:
```bash
python3 vol.py -f ch2.dmp windows.registry.hivelist
```
Identify the SYSTEM registry hive in the output. Note its offset.
## 5. Locate the Workstation Hostname
Windows stores the computer name in the SYSTEM registry hive.
The relevant registry path is:
```text
ControlSet001\Control\ComputerName\ComputerName
```
Use the registry `PrintKey` plugin:
```bash
python3 vol.py -f ch2.dmp windows.registry.printkey \
  --offset <SYSTEM_HIVE_OFFSET> \
  --key "ControlSet001\Control\ComputerName\ComputerName"
```
Replace `<SYSTEM_HIVE_OFFSET>` with the actual offset reported by the previous command.
Inspect the output for the `ComputerName` value. This is the workstation hostname.
## 6. Alternative Method: Volatility 2
If you are using Volatility 2, first identify the memory profile:
```bash
volatility -f ch2.dmp imageinfo
```
Use one of the suggested profiles, for example:
```bash
volatility -f ch2.dmp --profile=Win7SP1x86 envars
```
Look for the `COMPUTERNAME` environment variable.

Its value identifies the workstation hostname.
## 7. Result
The hostname recovered from the memory dump is:
```text
WIN-ETSA91RKCFP
```
**Validation answer:** `WIN-ETSA91RKCFP`

Author: Mr-incognito1202
