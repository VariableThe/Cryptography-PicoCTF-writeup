# Dachshund Attacks
## [Link to question](https://play.picoctf.org/practice/challenge/159?page=1&search=Dachshund)
## [Hint image file](https://mercury.picoctf.net/static/6b0ca75093bbcaf96c39eb47c048aef2/dachshund.jpg)
The question states: What if d is too small? Connect with nc mercury.picoctf.net 36463.<br>
Looking at the hint, it looks like he image of a dog.<br>
Using exiftool to look at metadata:
<pre>
exiftool dachshund.jpg
ExifTool Version Number         : 12.76
File Name                       : dachshund.jpg
Directory                       : .
File Size                       : 58 kB
File Modification Date/Time     : 2024:06:11 21:06:36+05:30
File Access Date/Time           : 2024:06:11 21:06:48+05:30
File Inode Change Date/Time     : 2024:06:11 21:06:36+05:30
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
XMP Toolkit                     : Adobe XMP Core 5.6-c140 79.160451, 2017/05/06-01:08:21
IPTC Digest                     : d41d8cd98f00b204e9800998ecf8427e
DCT Encode Version              : 100
APP14 Flags 0                   : [14], Encoded with Blend=1 downsampling
APP14 Flags 1                   : (none)
Color Transform                 : YCbCr
Image Width                     : 1200
Image Height                    : 650
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 1200x650
Megapixels                      : 0.780
</pre>
Nothing out of line, checking using binwalk:
<pre>
binwalk dachshund.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------

</pre>
Nothing at all<br>
Maybe the hint isn't in the details of the image, but comes from the image itself.<br>
But we can look into that later, for now, let's connect to the server.<br>
<pre>
nc mercury.picoctf.net 36463
Welcome to my RSA challenge!
e: 55379998972844046352865790680652799037349675291110681873760813795817324012999494121028022252092470280058646034046438592621694181868047770399586266034831698221859881913338249843453003243929281026064930484510827031906904533381214508705570783015115271823646464140540172717246964029628555227155120988513433691993
n: 62817108561656129503739920952078273196422120578598112117259670017864590229879049258911745739690612191940805022988374182143619241480303378143597598697996796685331703437349930229686952904514298999966729808608092182833077490181488103487177753685013818670225702780254301225772545190068420500937326159005450900567
c: 61842273820705131276292812643728613197074361765246267990458261085264372381677353492878743611759154266336005010036747107131408192691388118933395530446393295521576395368493510594183016427446757076764471303789834043215476810283875226654248840360951980245108295396141949581196610755401251858361180357335408926541
</pre>
It's an RSA. The question states, what if 'd' is too small. I believe it is refering to the 'd' value of the RSA encryption.<br>
Ok, so we can use the vulnerability of the small 'd' (private key value), we can brute force it, or just use factorization<br>
On second hand, maybe we don't need that, maybe the image contains the d value.<br>
First thing, we see a dog, a dog has 4 legs, how about using d as 4?<br>
Ok, so funny think, brute force is not really working, my fault to think of that anyways.<br>
So, let's wipe the board and think again, we have a photo of a dog as a hint, the dog is a weiner dog.<br>
Looking up weiner RSA leads us to [this](https://en.wikipedia.org/wiki/Wiener%27s_attack)<br>
Ok, we're not so lost now.<br>
The article includes 'Wiener has proved that the attacker may efficiently find d when d < 1/3*(N)^1/4'<br>
Ok, so it's less than whatever that operation gets us for the N value we have.<br>
Now, we just need a python code for the weiner attacking.<br>
Ok, so I found this [repo](https://github.com/pablocelayes/rsa-wiener-attack) online, looking for 'python weiner attack codes', yeah weiner attacks is a really great name.<br>
So I gitcloned the files and modified the 'RSAwienerHacker.py' by:
<pre>
 if t!=-1 and (s+t)%2==0:
                    print("Hacked!")
                    print(d)
                    return d
</pre>
I then run the code:
<pre>

</pre>
Nothing, the code's not working.<br>
I try reinstalling python, it still refuses to work<br>
I finally give up and look for other sources, I find a tool called RSActftool.<br>
I'm not able to clone it, i try about 5 times, on differnt os's as well.<br>
I though this was the end.<br>
But all of a sudden I had an Idea.<br>
I was unabe to run the python implementation code online or individually, because the author wrote codes in differnt places, what if I were to stich those codes together and run it as one single piece of code? Could it work?<br>
I spent about 10 minutes stiching it together and modifying the code to make this:
<pre>
import math
from typing import List, Tuple

# Types
CFListT = List[int]  # CF coefficients
CVListT = List[Tuple[int, int]]  # Convergents at each coefficient level

def rational_to_contfrac(x: int, y: int) -> Tuple[CFListT, CVListT]:
    """
    Converts a rational x/y fraction into
    a list of partial coefficients [a0, ..., an], and
    a list of convergents at each coefficient level [(n0, d0), (n1, d1), ...]

    Args:
        x (int): numerator of the given rational number
        y (int): denominator of the given rational number

    Returns:
        tuple[CFListT, CVListT]: a tuple of coefficients and convergents at each
        coefficient level
    """
    a = x // y
    cflist = [a]
    cvlist = [(a, 1)]
    ppn, ppd = 1, 0  # pre-pre numerator and denominator of convergent
    pn, pd = a, 1  # pre numerator and denominator of convergent
    while a * y != x:
        x, y = y, x - a * y
        a = x // y
        cflist.append(a)
        cn, cd = a * pn + ppn, a * pd + ppd
        cvlist.append((cn, cd))
        ppn, ppd = pn, pd
        pn, pd = cn, cd
    return cflist, cvlist

def contfrac_to_rational(frac: CFListT) -> Tuple[int, int]:
    ''' Convert continued fraction to rational number '''
    if len(frac) == 0:
        return (0, 1)
    num = frac[-1]
    denom = 1
    for x in frac[-2::-1]:
        num, denom = x * num + denom, num
    return (num, denom)

def is_perfect_square(n: int) -> int:
    '''
    If n is a perfect square it returns sqrt(n),
    otherwise returns -1
    '''
    h = n & 0xF  # last hexadecimal "digit"
    if h > 9:
        return -1  # return immediately in 6 cases out of 16.

    # Take advantage of Boolean short-circuit evaluation
    if h in {0, 1, 4, 9}:
        t = math.isqrt(n)
        if t * t == n:
            return t
    return -1

def egcd(a: int, b: int) -> Tuple[int, int, int]:
    '''
    Extended Euclidean Algorithm
    returns x, y, gcd(a,b) such that ax + by = gcd(a,b)
    '''
    u, u1 = 1, 0
    v, v1 = 0, 1
    while b:
        q = a // b
        u, u1 = u1, u - q * u1
        v, v1 = v1, v - q * v1
        a, b = b, a - q * b
    return u, v, a

def gcd(a: int, b: int) -> int:
    '''
    2.8 times faster than egcd(a,b)[2]
    '''
    a, b = (b, a) if a < b else (a, b)
    while b:
        a, b = b, a % b
    return a

def modInverse(e: int, n: int) -> int:
    '''
    d such that de = 1 (mod n)
    e must be coprime to n
    this is assumed to be true
    '''
    return egcd(e, n)[0] % n

def hack_RSA(e: int, n: int) -> int:
    '''
    Finds d knowing (e, n)
    applying the Wiener continued fraction attack
    '''
    _, convergents = rational_to_contfrac(e, n)
    
    for (k, d) in convergents:
        
        # Check if d is actually the key
        if k != 0 and (e * d - 1) % k == 0:
            phi = (e * d - 1) // k
            s = n - phi + 1
            # Check if the equation x^2 - s * x + n = 0 has integer roots
            discr = s * s - 4 * n
            if discr >= 0:
                t = is_perfect_square(discr)
                if t != -1 and (s + t) % 2 == 0:
                    print("Hacked!")
                    return d
    return None

def decrypt_message(ciphertext: int, d: int, n: int) -> int:
    '''
    Decrypts a given ciphertext using private key (d, n)

    Args:
        ciphertext (int): The encrypted message
        d (int): The private key exponent
        n (int): The modulus

    Returns:
        int: The decrypted message
    '''
    return pow(ciphertext, d, n)

e = 26193569043200580391604876271159252353905466417559092813329816924494386241437988247949552683226331052498138609102098904489988684870494771233583215948229229748114930822978205860266069376385262717407190334269824218862221599724861645127955913947470052376020766736126142593462229940652567402274934838641152850509
n = 123237694393968500725966505678701046123278478247757325548333030228861822676733591321273164259121740414335256214719347277668908251027764182249463335147193323513395420773740699814135683602569209757193165601481268185975077422027700346548122542558332995789866827714709230874390211590470934880842852233870681392151
ciphertext = 21432852827592610087459587275324538726600807073056376600416579794582955125252109415157882778680959401000924781879729886168616000016093823445577450995467372030056752872658784286395877129608136097333672796396402238224716154289400681885866635012533739915943156567711743681552371908180289250420063863353906892003 

# Hack RSA to find the private key
d = hack_RSA(e, n)
if d:
    print(f"Private key d: {d}")
    plaintext = decrypt_message(ciphertext, d, n)
    print(f"Decrypted message: {plaintext}")
else:
    print("Failed to hack RSA.")

</pre>
Then I ran the code, hoping for a miracle.<br>
It happened, I got back an integer<br>
<pre>
Hacked!
Private key d: 24661942732533274519994194826362733453781273842845628423749145773877254242997
Decrypted message: 198614235373674103788888306985643587194108045477674049828366797219789354877
</pre>
I had gotten the key, I was still highly skeptical if this was going to work as I had now spent over 5 hours on this CTF<br>
With baited breath I ran a code I made to use the corresponding ascii values of the message and print it, to ge the flag.<br>
This was the code:
<pre>
ciphertext = 198614235373674103788888306985643587194108045477674049828366797219789354877

# Convert ciphertext to bytes
ciphertext_bytes = ciphertext.to_bytes((ciphertext.bit_length() + 7) // 8, 'big')

# Convert bytes to text
plaintext = ciphertext_bytes.decode('ascii')

print("Decrypted message:", plaintext)
</pre>
The result?:
<pre>
picoCTF{proving_wiener_2635457}
</pre>
At that exact moment I was so overjoyed, I felt the weight of the world being lifted from my shoulders, my sanity returning again<br>
I quickly entered the flag and it was aacepted.<br>
I cannot stress how much I was frustrated over this, I was just so happy, that I can't even keep the professionality here.<br>
With the flag accepted, the task was now complete.<br>


