# miniRSA:
## [Link to question](https://play.picoctf.org/practice/challenge/31?page=1&search=miniRSA)
## [Image](https://jupiter.challenges.picoctf.org/static/eb5e6df8e14c52873cf88c582a1a4008/ciphertext)
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