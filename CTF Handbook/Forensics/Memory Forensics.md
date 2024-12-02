- There are plenty of traces of someone's activity on a computer, but perhaps some of the most valuble information can be found within memory dumps, that is images taken of RAM. These dumps of data are often very large, but can be analyzed using a tool called [Volatility](http://www.volatilityfoundation.org/)


## Volatility Basics
- Memory forensics isn't all that complicated, the hardest part would be using your toolset correctly. A good workflow is as follows:
	1. Run `strings` for clues
	2. Identify the image profile (which OS, version, etc.)
	3. Dump processes and look for suspicious processes
	4. Dump data related interesting processes
	5. View data in a format relating to the process (Word: .docx, Notepad: .txt, Photoshop: .psd, etc.)


### Profile Identification
- In order to properly use Volatility you must supply a profile with `--profile=PROFILE`, therefore before any sleuthing, you need to determine the profile using imageinfo.


### Dump Processes
- In order to view processes, the `pslist` or `pstree` or `psscan` command can be used.


### Process Memory Dump
- Dumping the memory of a process can prove to be fruitful, say we want to dump the data from notepad.exe.




### Other Useful Commands
- [There are plenty of commands](https://github.com/volatilityfoundation/volatility/wiki/Command-Reference) that Volatility offers but some highlights include:
	- `$ python vol.py -f IMAGE --profile=PROFILE connections`: view network connections
	- `$ python vol.py -f IMAGE --profile=PROFILE cmdscan`: view commands that were run in cmd prompt