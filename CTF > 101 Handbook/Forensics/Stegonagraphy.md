# Steganography
- Steganography is the practice of hiding data in plain sight. Steganography is often embedded in images or audio.
- You could send a picture of a cat to a friend and hide text inside. Looking at the image, there’s nothing to make anyone think there’s a message hidden inside it.

[![Steg with text](https://ctf101.org/forensics/images/steg-cat-text.png)](https://ctf101.org/forensics/images/steg-cat-text.png)
- You could also hide a second image inside the first.

[![Steg with an Image](https://ctf101.org/forensics/images/steg-cat-image.png)](https://ctf101.org/forensics/images/steg-cat-image.png)

## Steganography Detection
- So we can hide text and an image, how do we find out if there is hidden data?

[![Group of images](https://ctf101.org/forensics/images/steg-a-b-c-d.png)](https://ctf101.org/forensics/images/steg-a-b-c-d.png)
- FileA and FileD appear the same, but they’re different. Also, FileD was modified after it was copied, so it’s possible there might be steganography in it.
- FileB and FileC don’t appear to have been modified after being created. That doesn’t rule out the possibility that there’s steganography in them, but you’re more likely to find it in fileD. This brings up two questions:
	1. Can we determine that there is steganography in fileD?
	2. If there is, what was hidden in it?


## LSB Steganography
- File are made of bytes. Each byte is composed of eight bits.

[![Steganography Process Step 1](https://ctf101.org/forensics/images/steg-step-1.png)](https://ctf101.org/forensics/images/steg-step-1.png)
- Changing the least-significant bit (LSB) doesn’t change the value very much.

[![Steganography Process Step 2](https://ctf101.org/forensics/images/steg-step-2.png)](https://ctf101.org/forensics/images/steg-step-2.png)
- So we can modify the LSB without changing the file noticeably. By doing so, we can hide a message inside.


### LSB Steganography in Images
- LSB Steganography or _Least Significant Bit_ Steganography is a method of Steganography where data is recorded in the lowest bit of a byte.
- Say an image has a pixel with an RGB value of (255, 255, 255), the bits of those RGB values will look like
- By modifying the lowest, or least significant, bit, we can use the 1 bit space across every RGB value for every pixel to construct a message.

> rgb(255,255,255) is represented by `11111111` in binary. However, what difference does changing this to `11111110` make?

- The reason steganography is hard to detect by sight is because a 1 bit difference in color is insignificant as seen below.


![1 Bit Difference](https://ctf101.org/forensics/images/lsb-color-difference.png)

- Decoding LSB steganography is exactly the same as encoding, but in reverse. For each byte, grab the LSB and add it to your decoded message. Once you’ve gone through each byte, convert all the LSBs you grabbed into text or a file. (You can use your file signature knowledge here!)