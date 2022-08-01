# What happens in the background of my browser
![](https://www.wizcase.com/wp-content/uploads/2020/02/Internet-Explorer-logo.jpg)

in your browser background happens many operations to provide a protected environment let's know what happens .
 
First let's know some knowledges :

## Secure Sockets Layer (ssl) certificate

> is a small data file installed on a Web server that allows for a secure connection between the server and a Web browser.
## Encryption

> Encryption secures digital data using one or more mathematical techniques known as cryptography. The information input becomes unreadable through encryption as an [algorithm](https://www.investopedia.com/terms/a/algorithm.asp) converts the original text, known as plaintext, into an alternative form known as ciphertext.

*example*:

![encryption](https://cf-assets.www.cloudflare.com/slt3lc6tev37/4zLJngHjth92rb9VUrclZr/ec5b406b06e1fbee7dc0d5950789ce76/encryption-example.svg)

### Encryption types
**Symmetric encryption**

>this type include only one secret key to cipher and decipher information. symmetric encryption is an old and best-known technique. It uses a secret key that can be a number, a word or a string of random letters. It is a blended with the plain text of a message to change the content in a particular way.

*example:*

![encryption](https://www.ssl2buy.com/wiki/wp-content/uploads/2015/12/Symmetric-Encryption.png)

**Asymmetric Encryption**

> asymmetric encryption uses two keys to encrypt a plain text. one key is called the private key and the other key is called the public key. anything encrypted with the public key can only be decrypted with the private key; a public key cannot decrypt data if it was used to encrypt the data—only the private key can unlock that data.

*example:*

![encryption](https://www.ssl2buy.com/wiki/wp-content/uploads/2015/12/Asymmetric-Encryption.png)

# What happens in the background of browsing 
let's know what happens in your browser background when you visit a website using a ssl certificate,

 - first when you visit a https page your browser send request to the web server for make a https connection .
 - the web server respond with a **SSL CERTIFICATE** + **public key** *(we talk about asymmetric encryption)* .

> the web server tell for the browser this is my certificate  for check my identify and this is my public key for talk in secure environment.
> then browser take a certificate of the web server and check if  is ok, if not the communication fails.

 - after checking if the cert is ok, browser make a private key *(we talk about Symmetric encryption)* after make a private key the browser encrypt it with public key of the web server then browser send it for the web server .
 - browser decrypts the key content  completing the SSL handshake .


That’s it! All the above process happens when we hit any website uses ssl cert.

<center><img src="https://image.slidesharecdn.com/25-sales-interview-questions-150708211925-lva1-app6891/85/25-sales-interview-questions-to-recruit-superstar-reps-64-320.jpg?cb=1436458421"></center>
