## Forensics
- Has to do with finding hidden information
- Common types
	- Steganography
	- Packet Capture Analysis
	- Hard Disk Analysis


## Steganography
- The practice of hiding a message in a place where it wouldn't be expected
	- Images
	- Audio files
	- etc.

## Binary Numbers (Decimal <-> Binary)
- “Places” represent powers of two (instead of powers of 10 like in decimal).
	- 1: 1
	- 2: 10
	- 3: 11
	- 4: 100
	- 5: 101
	- 6: 110
	- 7: 111

![[Screenshot_20241115_215953.png]]

![[Screenshot_20241115_220012.png]]

![[Screenshot_20241115_220029.png]]

![[Screenshot_20241115_220043.png]]


## Color
- Red, green, and blue channels (usually 8 bits each)
![[Screenshot_20241115_220120.png]]


## How can this be used to hide stuff?
- The lower bits don't actually matter that much!
	- We can replace any bit plane (but probably the less significant ones) with a hidden image or even data encoded as pixels.


## Other places info can be hidden
- Metadata
	- Usually includes date and time, location, and camera information for a given photo
	- Flag can also be added as well
	- Look at the image "properties" or use "exiftool"

## OSINT
- "Open-Source Intelligence"
	- As opposed to proprietary/secret intelligence


## Common OSINT Problem Types
- Finding the GPS coordinates of an photograph
- Investigating accounts (that the organizers set up) on various social media platforms
- Finding deleted websites/posts/etc.


## OSINT Tools
- Wayback Machine
	- Saves snapshots of websites at various times, allows you to look through a website's history
- Reverse image serach
	- Try multiple search engines
- PimEyes
	- Facial recognition focused reverse image search


## Suggested Problems
- PicoCTF
	- Information
	- Wireshark doo dooo do doo...
	- St3g0
	- MSB (requires programming knowledge)
- WhenTaken/GeoGuessr/OpenGuessr/TimeGuessr