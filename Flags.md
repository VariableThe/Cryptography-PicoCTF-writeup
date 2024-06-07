# Flags:
## [Link to question](https://play.picoctf.org/practice/challenge/31?page=1&search=Flags)
## [Image](https://jupiter.challenges.picoctf.org/static/fbeb5f9040d62b18878d199cdda2d253/flag.png)

To start off, Lets download 'flag.png'<br>
Looking at the image, it's pretty obvious what the approach to solve the question is.<br>
We can see the brackets indicative of the picoCTF{XXX} blueprint, the number of symbols before the inital '{' is the same as 'picoCTF'<br>
My hypothesis is that every symbol represents a country's flag, and that country corresponds to a particualr letter.<br>
We can confirm this by the fact that the letter 'C' is represented by the same symbol when we cross reference the sequence of the symbols to the string 'picoCTF'<br>
