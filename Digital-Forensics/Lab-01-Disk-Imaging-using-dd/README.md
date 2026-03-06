Disk Imaging Lab
Overview

The Disk Imaging Lab is designed to teach and demonstrate the process of creating forensic disk images and analyzing them in a controlled environment. Disk imaging is a critical step in digital forensics, allowing investigators to capture an exact bit-by-bit copy of storage media for examination without altering the original evidence.

This lab covers:

Creating disk images using dd and FTK Imager.

Verifying disk integrity with hashing (MD5/SHA1/SHA256).

Mounting and analyzing images for evidence.

Documenting findings for forensic reporting.

Lab Objectives

Understand the importance of forensic disk imaging.

Learn how to create and verify disk images.

Perform basic analysis of disk images.

Document evidence in a professional manner suitable for investigations.

Tools Used

Linux (Kali Linux / Ubuntu)

FTK Imager (Windows)

Autopsy / Sleuth Kit

Hashing tools (md5sum, sha1sum, sha256sum)

Mounting tools (mount, ewfmount)

Commands & Steps
1️⃣ Identify Target Drive
lsblk
fdisk -l

Identify the device name (e.g., /dev/sdb) for the target disk.

2️⃣ Create Disk Image with dd
sudo dd if=/dev/sdb of=/mnt/forensics/disk_image.dd bs=4M status=progress

if = input file (source drive)

of = output file (destination image)

bs = block size

status=progress = shows real-time progress

This creates a bit-for-bit copy of the disk.

3️⃣ Verify Image Integrity
md5sum /mnt/forensics/disk_image.dd
sha256sum /mnt/forensics/disk_image.dd

Record these hash values to ensure the image is forensically sound.

4️⃣ Mount the Disk Image
sudo mkdir /mnt/disk_image
sudo mount -o loop,ro /mnt/forensics/disk_image.dd /mnt/disk_image
ls -la /mnt/disk_image

Mounting in read-only mode prevents accidental modification.

5️⃣ Analyze the Image

Examine file structure and directories.

Look for suspicious files (malware, hidden files, deleted files).

Use Autopsy or Sleuth Kit for deeper analysis:

fls -r /mnt/forensics/disk_image.dd
icat /mnt/forensics/disk_image.dd <inode>
Investigation Steps

Identify devices – Check connected drives and target disk.

Capture evidence – Create a disk image using dd or FTK Imager.

Verify evidence – Compute hash values to ensure integrity.

Mount image safely – Use read-only mode to prevent alteration.

Examine image – Search for hidden/deleted files and suspicious activity.

Document findings – Include screenshots, commands, and hashes.

Report – Prepare a forensic report summarizing the investigation.

Screenshots

Include screenshots of each step:

Disk identification with lsblk

dd imaging in progress

Hash verification outputs

Mounted image structure

Evidence extraction using Autopsy/Sleuth Kit

Best Practices

Always work on a copy, never the original disk.

Use write blockers if possible.

Document every command and observation.

Maintain a chain of custody for legal admissibility.

Validate your images using multiple hashing algorithms.

References

Carrier, B. File System Forensic Analysis, 2nd Edition.

Luttgens, J., Pepe, M., Mandia, K. Incident Response & Computer Forensics.

Autopsy User Guide: https://www.sleuthkit.org/autopsy/

Kali Linux Documentation: https://www.kali.org/docs/
