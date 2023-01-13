# Disk-Analysis-Autopsy---TryHackMe #

## Q1 - What is the MD5 hash of the E01 image? ##
```3f08c518adb3b5c1359849657a9b2079``` This is found by clicking on HASAN2.E01 under data sources and navigating to the Summary > Container tab
![Q1](https://user-images.githubusercontent.com/18509521/212192680-0c5f466f-5987-490b-b8ee-1d63eb39939b.png)

## Q2 - What is the computer account name? ##
```DESKTOP-0R59DJ3``` - Navigate to Operating System Information under the Results > Extracted Content
![Q2](https://user-images.githubusercontent.com/18509521/212192983-d9dcbe68-3c84-405e-9f1a-3a635ede45c9.png)

## Q3 - List all the user accounts. (alphabetical order) ##
```H4S4N, joshwa, keshav, sandhya, shreya, sivapriya, srini, suba``` This is found under Operating System User Account. Look at the path and if they are C:\Users\ then that is your answer.
![Q3](https://user-images.githubusercontent.com/18509521/212193493-25f284be-ebae-44b8-bef4-22c70a582e56.png)

## Q4 - Who was the last user to log into the computer? ##
```sivapriya``` Same place as the last question
![Q4](https://user-images.githubusercontent.com/18509521/212193718-d3791889-ee43-4f0f-8868-4d8dcb9f88bd.png)

## Q5 - What was the IP address of the computer? ##
```192.168.130.216``` We have seen that Look@Lan has been installed on the computer (the installer is in H4S4N'd Downloads) this may provide as with some IP information as this is a network monitoring tool and checking the registry where IP address' are stored resulted with nothing. We can look at the irunin.ini which is a configuration file and see if there is anything in there.
![Q5](https://user-images.githubusercontent.com/18509521/212213944-55d0fab9-ab4d-4298-923e-a7410af96d2f.png)

## Q6 - What was the MAC address of the computer? (XX-XX-XX-XX-XX-XX) ##
```08-00-27-2c-c4-b9``` We can find the MAC address in the same file under LANNIC, checking the registry where the NIC MAC address would be also resulted in nothing for this instance.
![Q6](https://user-images.githubusercontent.com/18509521/212214209-c2206785-64b1-49aa-94af-bf9cb6c48643.png)

## Q7 - What is the name of the network card on this computer? ##
```Intel(R) PRO/1000 MT Desktop Adapter``` This can be found in the registry ```C:\WINDOWS\system32\config\software\Microsoft\Windows NT\CurrentVersion\NetworkCards\``` To find this we need to navigate to C:\Windows\System32\Config Once we are in there we can find some registry keys. As our is Software we click on that one which will populate the Application tab. Afterwars we just continue to the pasted registry key path.
![Q7](https://user-images.githubusercontent.com/18509521/212210515-c6ab39f9-b78b-4690-a698-d98c1f7ae791.png)

## Q8 - What is the name of the network monitoring tool? ##
```look@lan``` I stumbled upon this one by accident. It is found under H4S4N's Downloads folder. There is an executable called lalsetup250.exe so I looked it up and found out it was a network monitoring tool.
![Q8](https://user-images.githubusercontent.com/18509521/212204357-bacbee3d-7371-4a80-8fc8-4b9d9334190c.png)

## Q9 - A user bookmarked a Google Maps location. What are the coordinates of the location? ##
```12°52'23.0"N 80°13'25.0"E``` Found under the web bookmarks tab
![Q9](https://user-images.githubusercontent.com/18509521/212200046-f17aede7-84e6-4d98-9012-824fe73d33d5.png)

## Q10 - A user has his full name printed on his desktop wallpaper. What is the user's full name? ##
```anto joshwa``` I went into recent documents and looked through how had access an image file then went to that directory and loaded the image.
![Q10](https://user-images.githubusercontent.com/18509521/212200642-ba74d3e0-9afe-4fda-bef0-6e606f20d326.png)

## Q11 - A user had a file on her desktop. It had a flag but she changed the flag using PowerShell. What was the first flag? ##
```flag{HarleyQuinnForQueen}``` Because we know she changed it using powershell we can to see if the powershell history file exists. This is located at ```%userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt``` As we can see, this file provides us with exactly what we needed.
![Q11](https://user-images.githubusercontent.com/18509521/212203490-46ae0ea2-3b31-4d1d-a711-01f237aa778e.png)

## Q12 - The same user found an exploit to escalate privileges on the computer. What was the message to the device owner? ##
```flag{i-hacked-you}``` Because we know that same user has found an exploit we can start looking around on their computer. If we navigate to their desktop we can find a suspicous file called exploit.ps1. Upon opening the script we can find the message.
![Q12](https://user-images.githubusercontent.com/18509521/212203811-4a31f398-ab81-49fd-83b7-49f6bccbd332.png)

## Q13 - 2 hack tools focused on passwords were found in the system. What are the names of these tools? (alphabetical order) ##
```lazagne, mimikatz``` To find this we need to navigate to ```/img_HASAN2.E01/vol_vol3/ProgramData/Microsoft/Windows/Windows Defender/Scans/History/Service/DetectionHistory/``` We can start looking through the files, there are multiple malicious files that have been detected so we will need to do some searching on what those files are.
![Q13-1](https://user-images.githubusercontent.com/18509521/212215401-665d975f-2087-40c4-b20f-ff8113aded47.png)
![Q13](https://user-images.githubusercontent.com/18509521/212215410-c6f11194-f4d4-4ade-912e-25784f7f7a74.png)

## Q14 - There is a YARA file on the computer. Inspect the file. What is the name of the author? ##
```benjamin delpy gentilkiwi``` As we know mimikatz is on H4S4N's Desktop we can navigate there and look at the contents of the zip file. Here we can find the kiwi_password.yar file. Look at the text in the document and we can get the answer.
![Q14](https://user-images.githubusercontent.com/18509521/212206201-cf7df1b5-6533-4863-8296-78b67e9233f2.png)


## Q15 - One of the users wanted to exploit a domain controller with an MS-NRPC based exploit. What is the filename of the archive that you found? (include the spaces in your answer) ##
```2.2.0 20200918 Zerologon encrypted.zip``` Upon searching what an MS-NRPC based exploit is I found out that it is called ZeroLogon. I remember seeing this file through my searches so I went back to Recent Documents and found it in there.
![Q15](https://user-images.githubusercontent.com/18509521/212206477-85125782-b0c1-48b3-8101-95d6d73982ed.png)




