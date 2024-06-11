# transposition-trial
## [link to question](https://play.picoctf.org/practice/challenge/312?page=1&search=transposition%20)
## [corrupted file](https://artifacts.picoctf.net/c/192/message.txt)
the question states:
<pre>
Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message.
Download the corrupted message here.
</pre>
Downloading the data, we see
<pre>
heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V091B0AE}2
</pre>
We can clearly make out that the first part is meant to say:
<pre>
The flad is picoCTF
</pre>
Using this intital block of unscrabled code, if we can figure out the way the jumbling occured, we can reverse engineer the correct flag.<br>
So, to make this easier on myself, I thought I would write a piece of code in python that would do that for me, turns out it look longer ~_~, Oh well.<br>
The code is:
<pre>
code = input("Enter the scrambled code: ")
cList = list(code)

for i in range(len(cList)):
    if (i+1) >= 3 and (i+1) % 3 == 0:
        cList[i-2], cList[i], cList[i-1] = cList[i], cList[i-1], cList[i-2]

unscrambled_code = ''.join(cList)
print(unscrambled_code)

quit()
</pre>
Using this, I got 'The flag is picoCTF{7R4N5P051N6_15_3XP3N51V3_109AB02E}'<br>
Submitting this works and the task is finished.<br>