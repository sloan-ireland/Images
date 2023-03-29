# TryHackMe CFT Collection Vol.1 Walkthrough

>*In this walkthrough I will go through the steps needed to complete the challenges CFT Collection Vol.1 Walkthrough. It’s an easy room, all the theory you’ll need is laid out very thoroughly by the creators, but in case you do get stuck, let’s go through the steps together.**


The room consists of a couple of tasks, touching on a different skill in some way so  you will have to find a flag that is hidden in some way. The flag format is THM{some_text_here}. Let’s start with the first task: cryptography.

## Task 2: What does the `base` say?
![Question 1](https://raw.githubusercontent.com/sloan-ireland/Images/main/27.03.2023_12.23.12_REC.png "Da Question")

The flag for this task is in some form of `base` which according to the hint is `base64`. We can also assume the form is proabably `base32` or `base64` because of the = at the end which these base forms commonly have due to the base form of `}` having an equal sign. This one of the more prevalent binary-to-text encoding schemes but there are many forms of ```base``` that can be used. 

If another `base` was used for encoding, you can determine the `base` by examining the characters used in the encoded string. Each `base` has its own set of characters that are used for encoding, so you can look for those specific characters to determine which `base` was used. Here are some examples of different bases and their associated characters:

 * ```base 16``` (hexadecimal): Uses the characters 0-9 and A-F to represent values from 0 to 15.
 * `base 32`: Uses the characters A-Z and 2-7 to represent values from 0 to 31.
* `base 58`: Uses a subset of the characters A-Z, a-z, and 1-9 to represent values from 0 to 57.
* `base 62`: Uses the characters A-Z, a-z, and 0-9 to represent values from 0 to 61.
* `base 85`: Uses a set of 85 ASCII characters to represent values from 0 to 84.

To actually get the plain text from base form for this question you can use the terminal command:
```
echo -n <base_text> | base64 -d
```
This command can be applied to some other base forms. Just switch out the   `base64` to `base<some_number>`. You may have to install this using `sudo` if it doesn't exist on your machine. 

If you can't figure out what base encoding was used or your computer doesn't have that base decode software installed, you can use a website such as [Cyberchef](https://cyberchef.org/).

## Task 3: Meta meta
![Q2](https://raw.githubusercontent.com/sloan-ireland/Images/main/29.03.2023_12.22.57_REC.png)
Given the name of this task we can assume we need to look at the metadata of the file. The [Findme.jpg](https://raw.githubusercontent.com/sloan-ireland/Images/main/Findme.jpg) file doesn't reveal anything at first glance so off to the terminal we go. We can use an EXIF tool to look at the metadeta using the following command:
```
exiftool Findme.jpg
```
You might have to install this tool via a `sudo` command. Alternatively, one can use an online tool such as [exifinfo](https://exifinfo.org/). 

Upon looking at the metadata we can clearly see the flag listed as the owner's name as seen below:\
<img src="https://raw.githubusercontent.com/sloan-ireland/Images/main/Screenshot%202023-03-29%20123508.png" alt="QR Code" width="`00%" height="75%"/>

Because the flag is in ASCII characters you can also use the command from task seven. Just make sure to switch out the file name correctly. 

## Task 4: Mon, are we going to be okay?
![Question 4](https://raw.githubusercontent.com/sloan-ireland/Images/main/29.03.2023_13.13.28_REC.png)


## Task #5: Erm......Magick
![Question2](https://raw.githubusercontent.com/sloan-ireland/Images/main/27.03.2023_16.44.47_REC.png)
As there is no given file to download or text to work with a safe guess is that the flag is hidden somewhere on the web page in the HTML. You can right click on different elements on the webpage to try and find the flag.
Click and highlight with the mouse. You never know what you can find. 

## Task #6: QRrrrr
![Qestion 5](https://raw.githubusercontent.com/sloan-ireland/Images/main/27.03.2023_16.55.00_REC.png)
We are given a file to download as seen in the image. Upon downloading the file, we can see it is a QR code which is shown below. Find out where it goes!
<img src="https://raw.githubusercontent.com/sloan-ireland/Images/main/QR%20COde.png" alt="QR Code" width="100%" height="25%"/>

## Task #7: Reverse it or read it
![Question 7](https://raw.githubusercontent.com/sloan-ireland/Images/main/28.03.2023_12.43.16_REC.png)
Once again we are provided a file with no prompt on any sort of process or action to do with it. The first logical thing to do with it is open it. Depending on the text editor you use, the file may not render meaning there are non-ASCII characters in the file. We can use the `cat` command to view the file in terminal. The flag is hidden somewhere in the readable characters. Searching the terminal can be a bit tedious so we can print only the wanted flag using the grep command below:
```
grep -o --binary-file=text -E 'THM{.*}' hello.hello
```
The `-o` flag returns only the matching segment of the line that matches the given pattern. The `-E` flag specifies the pattern using a regex expression that starts with THM followed by curly brackets with any number of characters in between them. The `--binary-file=text` segment forces grep to run on a binary file as grep will return an error otherwise. 

## Task #8: Another Decoding Stuff
![Question 8](https://raw.githubusercontent.com/sloan-ireland/Images/main/28.03.2023_13.04.27_REC.png)
Another base<some_number> flag! Yay! Now you get to practice using the terminal to decode this. Through eirther your skilled observation or the provided hint you have figured out this is in `base58`. Refer back to Task 2 to try and figure out the command for yourself (click on the button below if you need the answer).

<button onclick="alert('echo -n 3agrSy1CewF9v8ukcSkPSYm3oKUoByUpKG4L | base58 -d')">Task 8 Command</button>