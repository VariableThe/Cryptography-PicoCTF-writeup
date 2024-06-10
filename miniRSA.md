# miniRSA:
## [Link to question](https://play.picoctf.org/practice/challenge/31?page=1&search=miniRSA)
## [text file](https://jupiter.challenges.picoctf.org/static/eb5e6df8e14c52873cf88c582a1a4008/ciphertext)
To start off with we can take a look at the hint 1.

It has a link to the [wikipedia page explaining RSA's](https://en.wikipedia.org/wiki/RSA_(cryptosystem))<br>
Reading the articles does give a lot of information, but I'm still unaware about how I can decrypt the text using the linux terminal.<br>
Looking for 'how to decrypt RSA using linux terminal' gives us [this](https://www.google.com/search?q=how+to+decrypt+RSA+using+linux+terminal&sourceid=chrome&ie=UTF-8)<br>
I can see there is a lot mentioning of openssl. It's in every result.
Looking for openSSL on google give us [the site for openSSl](https://www.google.com/search?q=openSSL&sourceid=chrome&ie=UTF-8)
I ran openssl in the terminal hoping, it would ask me to download openSSL.
But instead I got this result:
<pre>
openssl
help:

Standard commands
asn1parse         ca                ciphers           cmp
cms               crl               crl2pkcs7         dgst
dhparam           dsa               dsaparam          ec
ecparam           enc               engine            errstr
fipsinstall       gendsa            genpkey           genrsa
help              info              kdf               list
mac               nseq              ocsp              passwd
pkcs12            pkcs7             pkcs8             pkey
pkeyparam         pkeyutl           prime             rand
rehash            req               rsa               rsautl
s_client          s_server          s_time            sess_id
smime             speed             spkac             srp
storeutl          ts                verify            version
x509

Message Digest commands (see the `dgst' command for more details)
blake2b512        blake2s256        md4               md5
rmd160            sha1              sha224            sha256
sha3-224          sha3-256          sha3-384          sha3-512
sha384            sha512            sha512-224        sha512-256
shake128          shake256          sm3

Cipher commands (see the `enc' command for more details)
aes-128-cbc       aes-128-ecb       aes-192-cbc       aes-192-ecb
aes-256-cbc       aes-256-ecb       aria-128-cbc      aria-128-cfb
aria-128-cfb1     aria-128-cfb8     aria-128-ctr      aria-128-ecb
aria-128-ofb      aria-192-cbc      aria-192-cfb      aria-192-cfb1
aria-192-cfb8     aria-192-ctr      aria-192-ecb      aria-192-ofb
aria-256-cbc      aria-256-cfb      aria-256-cfb1     aria-256-cfb8
aria-256-ctr      aria-256-ecb      aria-256-ofb      base64
bf                bf-cbc            bf-cfb            bf-ecb
bf-ofb            camellia-128-cbc  camellia-128-ecb  camellia-192-cbc
camellia-192-ecb  camellia-256-cbc  camellia-256-ecb  cast
cast-cbc          cast5-cbc         cast5-cfb         cast5-ecb
cast5-ofb         des               des-cbc           des-cfb
des-ecb           des-ede           des-ede-cbc       des-ede-cfb
des-ede-ofb       des-ede3          des-ede3-cbc      des-ede3-cfb
des-ede3-ofb      des-ofb           des3              desx
rc2               rc2-40-cbc        rc2-64-cbc        rc2-cbc
rc2-cfb           rc2-ecb           rc2-ofb           rc4
rc4-40            seed              seed-cbc          seed-cfb
seed-ecb          seed-ofb          sm4-cbc           sm4-cfb
sm4-ctr           sm4-ecb           sm4-ofb

</pre>
I think I may already have openSSl.<br>
To confirm this I ran 'openssl version'<br>
And got back:
<pre>
openssl version
OpenSSL 3.1.4 24 Oct 2023 (Library: OpenSSL 3.1.4 24 Oct 2023)
</pre>
I already have openssl version 3.1.4, now that it is confirmed I will move on to the applications of openSSl and how I can use it to decrypt the text.<br>
I also found [this video](https://youtu.be/wcbH4t5SJpg), and it looks promising, I will be back after looking into openSSL and studting a bit more about RSA.<br>
<br>
<br>
Ok, new update, the description of the file says 'Let's decrypt this: ciphertext? Something seems a bit small.'
This is the ciphertext:
<pre>

N: 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e: 3

ciphertext (c): 2205316413931134031074603746928247799030155221252519872650080519263755075355825243327515211479747536697517688468095325517209911688684309894900992899707504087647575997847717180766377832435022794675332132906451858990782325436498952049751141 
</pre>

We can see that the e is quite small, as the hint 2 says, because of the small value of e the security of the encryption isn't very strong, we can leverage this to our advantage<br>
and thereby decrypt the message without the private key.<br>
Although I'm still not sure on how to go about that, but still progress is always positive.<br>
