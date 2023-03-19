---
title: "How to configure BitLocker with TPM, PIN, and USB StartupKey"
date: 2023-03-18T22:40:26-04:00
draft: false
---

The BitLocker GUI in the Windows 7 Control Panel supports TPM + PIN and TPM + USB StartupKey but not TPM + PIN + USB StartupKey. This configuration requires editing Group Policy and using the command line tool manage-bde.

This guide is intended for a sophisticated audience. The consequences of following the procedure are not discussed here.

## Environment

Variations on this also work, such as Windows 7 Enterprise or a USB hard drive instead of one of the flash drives.

- Windows 7 Ultimate
- TPM 1.2 chip on motherboard
- 2 USB flash drives
- An administrator account (use the same account throughout the entire process)

## 1. Setup Group Policy

In *Search programs and files* on the Start Menu, type *gpedit.msc*. Hold &lt;Shift&gt; + &lt;Ctrl&gt; and press &lt;Enter&gt; to run as an administrator.

Open *Computer Configuration -> Administrative Templates -> Windows Components -> BitLocker Drive Encryption -> Operating System Drives*.

Open *Require additional authentication at startup*. Be careful to avoid the similarly named *Require additional authentication at startup (Windows Server 2008 and Windows Vista)*.

Enable the policy.

Uncheck *Allow BitLocker without a compatible TPM*.

Set *Configure TPM startup*, *Configure TPM startup PIN*, and *Configure TPM startup key* to *Do not allow...*.

Set *Configure TPM startup key and PIN* to *Require startup key and PIN with TPM*.

There are several other Group Policies that can be configured but are not required, including:

- *Allow enhanced PINs for startup*
- *Configure TPM platform validation profile*
- *Choose drive encryption method and cipher strength* (outside the Operating System Drives folder)

In *Search programs and files* run *gpupdate* as an administrator.

## 2. Setup the TPM

Open *Control Panel -> BitLocker -> Manage TPM* (on the bottom left).

Initialize the TPM using the utility. A restart will probably be required. Follow the directions in the utility carefully as well as any directions that appear during the restart.

If a restart was required, logon. The utility will automatically open to complete the setup. Backup the TPM owner key using the utility when prompted.

## 3. Add a Recovery Key

In *Search programs and files* run *cmd* as an administrator.

Insert a USB flash drive and note the drive letter assigned to it.

Run the command below to add a Recovery Key. Replace F with the drive letter assigned to the USB flash drive. C is the drive to be encrypted. F is the location to save the Recovery Key.

*manage-bde -protectors -add C: -RecoveryKey F:*

The command should result in the output below. My key IDs have been redacted.

> BitLocker Drive Encryption: Configuration Tool version 6.1.7601
> 
> Copyright (C) Microsoft Corporation. All rights reserved.
> 
> Key Protectors Added:
> 
> Saved to directory F:
> 
> External Key:
> 
> ID: REDACTED
> 
> External Key File Name:
> 
> REDACTED

Remove the USB flash drive and store it securely. The Recovery Key can be used to access the drive without the TPM and PIN. This USB flash drive is not the one that will be used to boot the computer for normal use.

## 4. Add the TPM, PIN, and USB StartupKey

Insert the second USB flash drive and note the drive letter assigned to it.

Run the command below to add a TPM, PIN, and USB StartupKey. Replace REDACTED with your PIN. Although a BitLocker PIN can contain spaces, it is easier to avoid spaces when setting the PIN via the command line. Replace E with the drive letter assigned to the USB flash drive. C is the drive to be encrypted. E is the location to save the StartupKey.

*manage-bde -protectors -add C: -TPMandPINandStartupKey -tp REDACTED -tsk E:*

The command should result in the output below. My key IDs have been redacted.

> BitLocker Drive Encryption: Configuration Tool version 6.1.7601
> 
> Copyright (C) Microsoft Corporation. All rights reserved.
> 
> Key Protectors Added:
> 
> Saved to directory E:
> 
> TPM And PIN And Startup Key:
> 
> ID: REDACTED
> 
> External Key File Name:
> 
> REDACTED

Do not remove the USB flash drive.

## 5. Encrypt the drive

Run the command below to perform a hardware check and encrypt the drive. C is the drive to be encrypted.

*manage-bde -on C:*

The command should result in the output below.

> BitLocker Drive Encryption: Configuration Tool version 6.1.7601
> 
> Copyright (C) Microsoft Corporation. All rights reserved.
> 
> Volume C: []
> 
> [OS Volume]
> 
> ACTIONS REQUIRED:
> 
> 1 Insert a USB flash drive with an external key file into the computer.
> 
> 2 Restart the computer to run a hardware test.
>
> (Type "shutdown /?" for command line instructions.)
> 
> 3 Type "manage-bde -status" to check if the hardware test succeeded.
> 
> NOTE: Encryption will begin after the hardware test succeeds.

Restart your computer as instructed. Logon after the restart.

If the hardware test passed the drive will be encrypted. A GUI will show the encryption progress. If the hardware test failed the drive will not be encrypted.

## References

[Manage-bde.exe Parameter Reference](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-7/dd875513(v=ws.10)?redirectedfrom=MSDN)
