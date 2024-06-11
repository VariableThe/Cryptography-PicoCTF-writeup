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
