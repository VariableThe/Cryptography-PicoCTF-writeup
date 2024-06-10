# Flags:
## [Link to question](https://play.picoctf.org/practice/challenge/31?page=1&search=Flags)
## [Image](https://jupiter.challenges.picoctf.org/static/fbeb5f9040d62b18878d199cdda2d253/flag.png)

To start off, Lets download 'flag.png'<br>

Looking at the image, it's pretty obvious what the approach to solve the question is.<br>
We can see the brackets indicative of the picoCTF{XXX} blueprint, the number of symbols before the inital '{' is the same as *'picoCTF'*<br>

My hypothesis is that every symbol represents a country's flag, and that country corresponds to a particualr letter.<br>
We can confirm this by the fact that the letter 'C' is represented by the same symbol when we cross reference the sequence of the symbols to the string 'picoCTF'<br>

A quick search on the web for country's flags leads to [this site](https://www.worldometers.info/geography/flags-of-the-world/)

Ok, so there doesn't appear to be flags that match the look of the symbols. Maybe it has something to do with the color scheme? Or perhaps maybe the color itself?

After a lot, and I mean a lot of searching, I think I may have found a lead.
The symbol used for 'c' in the encoded flag has blue, white, red, white and blue colours in this order from top to bottom.
I found that the flag of the 'DPRK' suits this order as well, and since the country starts with a 'D' the encoding might just be rot1 plus a random flag of the country that starts with the rot1 letter.
So to confirm this we can take any one of them and try matching them with any countries flags and those should start with The letter of the alphabet after the one that the symbol substitutes for.

Ok, after trying this for about 3 flags, I've given up, I can't seem to find the flags that match with the symbols in the cipher
I'm thinking about how I've pre isolated my search to just flags of territories, maybe they're not flags of territiories at all, maybe I'm chasing the wrong lead.

After looking up on google for [square flag with blue boundry and white square](https://www.google.com/search?q=square+flag+with+blue+boundry+and+white+square&sca_esv=f87e2b13d9f53375&sxsrf=ADLYWIKj481DwDXFKuGqZ_2oV4OR8m4lCg:1718000123039&ei=-5lmZvCGAsCo4-EPwaWV-Ac&ved=0ahUKEwiw8LqYsdCGAxVA1DgGHcFSBX8Q4dUDCBA&uact=5&oq=square+flag+with+blue+boundry+and+white+square&gs_lp=Egxnd3Mtd2l6LXNlcnAiLnNxdWFyZSBmbGFnIHdpdGggYmx1ZSBib3VuZHJ5IGFuZCB3aGl0ZSBzcXVhcmUyChAhGKABGMMEGAoyChAhGKABGMMEGApI7BNQuwlYuxJwAXgBkAEAmAHqAqABwQ2qAQUyLTQuMrgBA8gBAPgBAZgCAqAC-QHCAgoQABiwAxjWBBhHmAMA4gMFEgExIECIBgGQBgiSBwUxLjAuMaAHriI&sclient=gws-wiz-serp#vhid=fwv0X92y9tOhNM&vssid=l)
I've found the first flag (the one that substitues for P)
And the link from where the flag is had lead me to [National Park Service](https://www.nps.gov/media/photo/gallery-item.htm?id=f6e69e77-5091-4023-8d1b-932bd5bcf89e&gid=791FF38A-DF86-4963-932F-EE7641143F49)
And wouldn't you know it, this contains the flags we've been looking for.
Now, the only step left is to decode the flag.

Ok, I'm facing an isssue, although majority of the flags are there on the NPS site, some aren't.
After looking up ICS flags on wikipedia, we get [this](https://en.wikipedia.org/wiki/International_maritime_signal_flags)
And here we find that the number flags have an additional set of flags, set by NATO, and they match the symbols.
Using these flags, to substitute, the flag is:
<pre>
PICOCTF{F1AG5AND5TUFF}
</pre>
And that is Flags done.
