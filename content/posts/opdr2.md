---
title: "Opdracht 2"
date: 2018-03-07T13:08:54+01:00
draft: false
---

## 1.Sniffing at RSA
Het begin van opdracht 2 begon met een kennismaking over priem getallen. Door een zo hoog mogelijk priem getal te nemen des te kleiner de kans was dat de encryptie te kraken is.
<!--more-->

```
----------------------------------------------
Encryptie
m       = 289
E(m)    = 289^3 (mod 319)
        = 115
----------------------------------------------
Decryptie
c       = 115
d(c)    = 115^187 (mod 319) = 289
----------------------------------------------
```

Door het maken van de tweede opdracht kwamen we erachter dat wanneer de m waarde groter is dan de modulo de uitkomst van de encryptie en decryptie niet gelijk is.


## 2.Almost real RSA
Q: contains a working RSA implementation. Get it running and show that it can be used for 1. confidentiality ad 2. integrity. Appreciate how few lines of code this extremely important algorithm is.

A: The program generates a key pair and using  the public key to encrypt ensures confidentiality and encrypting with the private key ensures with integrity.


## 3.Certificates

### 3.1 What is a certificate? Explain in your own words.
Een certificaat is een bewijs voor authenticity.

### 3.2 What is a self-signed certificate? Explain in your own words.
Een certificaat die is ondertekend door de partij die het gebruikt.

### 3.3 Creating your own self-signed certificate
Om ons eigen certificaat te generen hebben we de stappen gevolgd uit de opdracht. We hebben openssl geinstalleerd. Daarna de environment variable aangemaakt. Daarna konden we openssl gebruiken binnen powershell

### 3.4 Create a simple nodejs server
Om de nodejs server aan te maken moesten we als eerste stap nodejs installeren. Gelukkig hadden wij allebei dit al gedaan dus konden we deze stap overslaan. Vervolgens zijn de we aangegeven repository uit de opdracht gaan clonen naar onze computer. Nadat de server draaide hebben we de laatste stap gevolgd namelijk de server.js aangepast volgens de link die was toegevoegd in het document.

### 3.5 Verify using wireshark
Om ook daadwerkelijk te controleren of de verbinding correct was ingesteld en dat confidentiality gegarandeerd is, hebben we via wireshark onze connectie getest. 

![Wireshark Capture] (/images/opdr2/wireshark.png)
Zoals hierboven te zien is valt de data niet te onderscheppen, hierdoor weten wij zeker dat confidentiality bewaard blijft. 

### 3.6 Install private key and certificate in wireshark
Als laatste hebben we het certificaat toegevoegd binnen wireshark aan de hand van de hulp linkjes.

## 4.Cryptographic hash functions

### 4.1 which 3 properties are used to define the security level of a cryptographic hash function? Explain each of these in your own words.

* Het is makkelijk om een hash uit te rekenen
* Het is extreem moeilijk om een tekst te vinden waar de zelfde hash uitkomt.
* Het is extreem onwaarschijnlijk dat twee net iets verschillende berichten de zelfde hash hebben.

### 4.2 use the openssl library to create a hash using SHA-256 
In opdracht 4.2 moesten wij een hash generen van een stuk tekst dit hebben wij op de volgende manier gedaan.

```
echo "Het hele stuk tekst" | .\openssl dgst - sha256
```

De uitkomst daarvan was het onderstaande:

`128ee56b75d4f1310c429f0407f0629975e534519cfff6bb45999411cb865dec` = de hash

## 5.Digital signature

### 5.1 change one character of the message and create a SHA-256 hash of the same message. Verify that the hashes are not equal: we can detect tampering!

Nu moesten we de tekst van de vorige opdracht gaan veranderen en daarna opnieuw een hash genereren. hieruit moest blijken dat de hash daadwerkelijk was veranderd en dus niet het zelfde was gebleven.
We hebben nogmaals de opdracht uitgevoerd en een aantal karakters in de tekst veranderd de output was de onderstaande nieuwe hash.

`9900288a5de676a0945d58ec0ab4030a9c1c69c6b6aa6ac69f0ca629106c0f38` = de nieuwe hash

#### 5.1.2 However, this is not sufficient to guarantee integrity! How do we know that the message is authentic, meaning that it is not tampered with, but also that it actually originates from the lovely Alice and not evil Carol?

There are two solution to this:

*	Symmetric digital signature based on a shared secret
*	Asymmetric digital signature

### 5.2 we’re are going to focus on the asymmetric digital signature. Recall from Security 1 how an asymmetric digital signature works and perform the algorithm manually using openssl.

`openssl rsautl -sign -in hash.txt -inkey localhost.key -out sig`

[Opdracht 4](/posts/opdr4)
