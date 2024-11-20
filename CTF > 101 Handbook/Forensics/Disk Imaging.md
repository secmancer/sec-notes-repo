# Disk Imaging
- A forensic image is an electronic copy of a drive (e.g. a hard drive, USB, etc.). It’s a bit-by-­bit or bitstream file that’s an exact, unaltered copy of the media being duplicated.
- Wikipedia said that the most straight­forward disk imaging method is to read a disk from start to finish and write the data to a forensics image format. “This can be a time-consuming process, especially for disks with a large capacity."


## Checksum
- Validating files is one of the most important aspects of disk forensics. This hash will change if any part of file is changed, making it great for catching alterations to the original source.
- We can use tools like `md5sum` or `sha256sum` from the command line to generate the hashes of a file. _Observe the different hash when the file is altered._ [![Hash](https://ctf101.org/forensics/images/hash.gif)](https://ctf101.org/forensics/images/hash.gif)

## Write Blocker
- It's common practice to use a write blocker before imagining a disk. This prevents unintended writes to the disk to maintain integrity.
- [Kali Linux](https://www.kali.org/docs/general-use/kali-linux-forensics-mode/) has a "forensics" mode that features a write blocker and is designed for all sorts of forensics in mind.


## Why image a disk?
- Prevents tampering with the original data­ evidence
- Allows you to play around with the copy, without worrying about messing up the original