---
title: Cryptography notes
top: false
cover: false
toc: true
mathjax: true
date: 2020-07-12 23:19:52
categories: Tech
tags: 
    - Security
password:
---

## Digital signature
<!--more-->

![](image-20200708104031335.png)

1. Bob has private key and public key, and sends the public key to Alice.
2. Bob generates a plaintext memo, and uses hash algorithm on it to have a digest.
3. Then Bob encrypts the digest using his private key and gets a digital signature.
4. Bob then sends the digital signature along with the memo (**Note: the memo is not encrypted**) to Alice.
5. Alice uses Bob's public key and decrypt the digital signature to gets the digest.
6. Alice then uses the same hash algorithm on the plaintext memo and gets another digest.
7. Alice compares both digests, if they are same, then Alice can be confident that the memo has not been changed.

**NOTE: ** using digital signature does not encrypt the message itself, if Bob wants to encrypt the message, he will need to use Alice's public key to encrypt it.

## Digital Certificate

Ditital cert is issued by a third party, and it's based on trust and it verifies that the digital signature is truly signed by the claims singer. It contains information as:

1. Certificate owner's name;
2. Owner's public key and its expiration date;
3. Certificate issuer's name;
4. Certificate issuer's digital signature

![](image-20200708110748416.png)

##　SSL Certificate

![](image-20200708113856166.png)

**SSL certificate** is a web server's digital certificate, issued by a third party, and verifies the identity of web server and it's public key.

For example, I want to go to https://yahoo.com and I want to make sure all communications are secure.

1. Browser requests secure pages from a yahoo web server;
2. Yahoo server sends its public key with the SSL certificate, signed by a third party (CA);
3. Client check with CA for the to make sure the cert is valid (common browser already got public keys installed from many popular CAs);
4. Exchange the secret: client browser creates symmetric key, it uses web server's public key to encrypt the secret and sends it;
5. Server uses its private key to decrypt the secret, now the server gets the shared key;
6. From now on, the messages between client and server will be encrypted and decrypted using the shared key.



## PKI (Public Key Infrastructure)

A framework for managing digital certificates and public key encryption

![](image-20200708152328368.png)







## SSL/TLS handshaking protocol

1. Client sends "ClientHello" with SSL/TLS version, cryptographic algorithms and data compression methods that it supports;
2. Server responds with "ServerHello" with cryptographic algorithm agreement, session ID, digital cert and its public key;
3. Client checks with server's CA to confirm and establish trust;
4. ClientKeyExchange - client sends a shared secret key encrypted by the server's public key;
5. Client sends a "Finished" message with the shared secret key - handshake complete;
6. Server responds with a "Finished" message indicating handshake is completed.

![](image-20200708153106778.png)



## Self signed certificate

Self signed SSL certificate does not mean it's necessarily less secure than purchased SSL certificates

All SSL certificates just ensure that the identity of the website is certified and the traffic between your browser and the web server are encrypted. They won't ensure your data won't be stolen.



## Revocation of certificates



Situation causes revocation: 

1. Certificate is no longer used;
2. Details of certificate are changed;
3. The certificate owner's private key was compromised;
4. Certificates were stolen from CA



