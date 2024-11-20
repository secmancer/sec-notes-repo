- Metadata is data about data. Different types of files have different metadata. The metadata on a photo could include dates, camera information, GPS location, comments, etc. For music, it could include the title, author, track number and album. CTF challenges often have you looking for specific clues in the metadata of a file (especially media files).

> EXIF Data is metadata attached to photos which can include location, time, and device information.


## How do I find it?
- One of our favorite tools is [`exiftool`](https://exiftool.org/), which displays metadata for an input file: - File size - Dimensions (width and height) - File type - Programs used to create (e.g. Photoshop) - OS used to create (e.g. Apple)


## Timestamps
- Timestamps are data that indicate the time of certain events (MAC): - Modification – when a file was modified - Access – when a file or entries were read or accessed - Creation – when files or entries were created


### Types of timestamps
- Modified
- Accessed
- Created
- Date Changed (MFT)
- Filename Date Created (MFT)
- Filename Date Modified (MFT)
- Filename Date Accessed (MFT)
- INDX Entry Date Created
- INDX Entry Date Modified
- INDX Entry Date Accessed
- INDX Entry Date Changed


### Why do we care?
- Certain events such as creating, moving, copying, opening, editing, etc. might affect the MAC times. If the MAC timestamps can be attained, a timeline of events could be created.


### Timeline Patterns
- There are plenty more patterns than the ones introduced below, but these are the basics you should start with to get a good understanding of how it works, and to complete this challenge.

[![Timeline 1](https://ctf101.org/forensics/images/timeline-1.png)](https://ctf101.org/forensics/images/timeline-1.png) [![Timeline 2](https://ctf101.org/forensics/images/timeline-2.png)](https://ctf101.org/forensics/images/timeline-2.png) [![Timeline 3](https://ctf101.org/forensics/images/timeline-3.png)](https://ctf101.org/forensics/images/timeline-3.png) [![Timeline 4](https://ctf101.org/forensics/images/timeline-4.png)](https://ctf101.org/forensics/images/timeline-4.png) [![Timeline 5](https://ctf101.org/forensics/images/timeline-5.png)](https://ctf101.org/forensics/images/timeline-5.png)