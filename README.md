# Period-4

1.Explain basic security terms like authentication, authorization, confidentiality, integrity, SSL/TLS and provide examples of how you have used them:

Authentication is the process of determining whether someone or something is, in fact, who or what it is declared to be.
Logically, authentication precedes authorization (although they may often seem to be combined). The two terms are often used synonymously but they are two different processes.


Authentication vs. authorization
Authentication is a process in which the credentials provided are compared to those on file in a database of authorized users’ information on a local operating system or within an authentication server. If the credentials match, the process is completed and the user is granted authorization for access. The permissions and folders returned define both the environment the user sees and the way he can interact with it, including hours of access and other rights such as the amount of allocated storage space.

The process of an administrator granting rights and the process of checking user account permissions for access to resources are both referred to as authorization. The privileges and preferences granted for the authorized account depend on the user’s permissions, which are either stored locally or on the authentication server. The settings defined for all these environment variables are set by an administrator.


Once the user is authenticated then some permissions are granted to him to access some content like for example
his/hers profile or orders if the website is a commerce site. Usually (if not always) there many types of users
that have different permissions to access segments of a website, normally a user shouldn't be able to add, edit,
delete other users and if he tries to access a directory or a page that does so he/she should get a 401 error
mentioning that the user is unauthorized to perform some action.


Confidentiality is some kind of reassurance that the bridge of communication of sensitive information from the user/client to server
and vice-versa is safe and no data is leaking, getting "sniffed" or tampered with in between. This is important
because if username and password are liked then there is a threat that the user on the other end is not the expected one.
So as a good rule of thumb is to never store passwords in databases to prevent this phenomenon. Instead a hashed value
(always with the same hashing algorithm)and usually salted (salting a pasword is when we add a long string of
characters to the password before hashing it) is stored to the database.


Integrity involves maintaining the consistency, accuracy, and trustworthiness of data over its entire life cycle.
Data must not be changed in transit, and steps must be taken to ensure that data cannot be altered by
unauthorized people (for example, in a breach of confidentiality).
Version control maybe used to prevent erroneous changes or accidental deletion by authorized users becoming a problem.


SSL/TSL are cryptographic protocols designed to provide communications security over a computer network.
These certificates are provides by approved licenced providers that are thoght to be credible and trust worthy.
A symmetric key exists in both ends of a transaction/communication to ensure that this conversation is private.

------------------------------------------------

2. Explain basic security threads like: Cross Site Scripting (XSS), SQL Injection and whether something similar to SQL injection is possible with NoSQL databases like MongoDB, and DOS-attacks. Explain/demonstrate ways to cope with these problems:

2.1 XSS: Cross Site scripting is when you write scripts directly in a guestbook or other places on a webpage which is then being runned when other people visits the page - thereby giving a lot of possibilities for the scriptkid to gain access to user sensitive data.

2.2 SQL Injection: Somewhat the same method as with XSS - a page where you can write SQL statements directly in a login or a search field thereby being able to use the 1=1 method to gain priviliges to do what ever you want via SQL.

2.3 DDOS: Denial Of Service attacks is where you send a lot of requests to a server using a bot network to either deny 'real' trafic access or to crash the server. Threats using a NoSQL database: There is not something directly similar to SQL injection with a NoSQL database, but there are other security issues - e.g. with MongoDB you dont have a admin password thereby having the database 'exposed' if the communicationport 27017 and 28017 is open on the server.
----------------------------------------------------

3. Explain, at a fundamental level, the technologies involved, and the steps required initialize a SSL connection between a browser and a server and how to use SSL in a secure way:

SSL (Secure Sockets Layer) is a standard security technology for establishing an encrypted link
between a server and a client; typically a web server and a browser.

SSL allows sensitive information such as credit card numbers, social security numbers, and login credentials to be transmitted securely. Normally, data sent between browsers and web servers is sent in plain text—leaving you vulnerable to eavesdropping. If an attacker is able to intercept all data being sent between a browser and a web server they can see and use that information.

More specifically, SSL is a security protocol. Protocols describe how algorithms should be used; in this case, the SSL protocol determines variables of the encryption for both the link and the data being transmitted.

 When a browser attempts to access a website that is secured by SSL, the browser and the web server establish
 an SSL connection using a process called an “SSL Handshake” (see diagram below).
 
 BROWSER                            SERVER
    |                                   |
    |-----1. Client hello-------------->| (Browser connects to a web server (website) secured with SSL (https).
    |<-----2. Server hello--------------|  Browser requests that the server identify itself.)
    |                                   |
    |(3. client authenticate server)    |
    |                                   | (Server sends a copy of its SSL Certificate, including the server’s public key.)
    |-----4. Pre-master secret--------->|
    |-----5. Client certificate-------->|
    |                                   | (Browser checks the certificate root against a list of trusted CAs and that
    |   (6. server authenticates client)|  the certificate is unexpired, unrevoked, and that its common name is valid
    |                                   |  for the website that it is connecting to. If the browser trusts the
    |<-----7. Session key creation------|  certificate, it creates, encrypts, and sends back a symmetric session key
    |-----8. Client finished----------->|  using the server’s public key.)
    |<-----9. Server finished-----------|
    |                                   | (Server decrypts the symmetric session key using its private key and sends
    |<--10. SSL handshake COMPLETED---->|  back an acknowledgement encrypted with the session key to start the encrypted session.)
    |                                   |
    |<-11.Exchange messages(ENCRYPTED)->| (Server and Browser now encrypt all transmitted data with the session key.)
    |                                   |
 Because encrypting and decrypting with private and public key takes a lot of processing power, they are only
 used during the SSL Handshake to create a symmetric session key. After the secure connection is made,
 the session key is used to encrypt all transmitted data.
 -----------------------------------------
 
4. Explain and demonstrate ways to protect user passwords on our backends, and why this is necessary.

What is password hashing?

Hash algorithms are one way functions. They turn any amount of data into a fixed-length "fingerprint" that cannot be reversed. They also have the property that if the input changes by even a tiny bit, the resulting hash is completely different (see the example above). This is great for protecting passwords, because we want to store passwords in a form that protects them even if the password file itself is compromised, but at the same time, we need to be able to verify that a user's password is correct.

The general workflow for account registration and authentication in a hash-based account system is as follows:

1.The user creates an account.
2.Their password is hashed and stored in the database. At no point is the plain-text (unencrypted) password ever written to the hard drive.
3.When the user attempts to login, the hash of the password they entered is checked against the hash of their real password (retrieved from the database).
4.If the hashes match, the user is granted access. If not, the user is told they entered invalid login credentials.
5.Steps 3 and 4 repeat everytime someone tries to login to their account.

hash("hello") = 2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824
hash("hbllo") = 58756879c05c68dfac9866712fad6a93f8146f337a69afe7dd238f3364946366
hash("waltz") = c0e81794384491161f1777c232bc6bd9ec38f616560b120fda8e90f383853542

The principal difference - MD5 and other hash functions designed to verify data have been designed to be fast, and bcrypt() has been designed to be slow.

When you are verifying data, you want the speed, because you want to verify the data as fast as possible.

When you are trying to protect credentials, the speed works against you. An attacker with a copy of a password hash will be able to execute many more brute force attacks because MD5 and SHA1, etc, are cheap to execute.

bcrypt in contrast is deliberately expensive. This matters little when there are one or two tries to authenticate by the genuine user, but is much more costly to brute-force.

source:

https://crackstation.net/hashing-security.htm

http://stackoverflow.com/questions/7072478/whats-the-difference-between-bcrypt-and-hashing-multiple-times
---------------------------------------

5. Explain about JSON Web Tokens (jwt) and why they are very suited for a REST-based API:

JSON Web Token (JWT) is a compact URL-safe means of representing claims to be transferred between two parties.
 The claims in a JWT are encoded as a JSON object that is digitally signed using JSON Web Signature (JWS).
 A JWT consists of three main components: a header object, a claims object, and a signature. These three properties
 are encoded using base64, then concatenated with periods as separators.
 JSON Web Tokens (JWT) are a more modern approach to authentication. As the web moves to a greater separation between
 the client and server, JWT provides a wonderful alternative to traditional cookie based authentication models.

ADVANTAGES:
 - Cross-domain / CORS: cookies + CORS don't play well across different domains. A token-based approach allows you to
   make AJAX calls to any server, on any domain because you use an HTTP header to transmit the user information.
 - Stateless: there is no need to keep a session store, the token is a self-contained entity that conveys all the
   user information.
 - CDN: you can serve all the assets of your app from a CDN (e.g. javascript, HTML, images, etc.), and your
   server side is just the API.
 - Decoupling: you are not tied to a particular authentication scheme. The token might be generated anywhere, hence
   your API can be called from anywhere with a single way of authenticating those calls.
 - Mobile ready: when you start working on a native platform (iOS, Android, Windows 8, etc.) cookies are not ideal
   when consuming a secure API (you have to deal with cookie containers). Adopting a token-based approach
   simplifies this a lot.
 - CRSF: since you are not relying on cookies, you don't need to protect against cross site requests.

 Client application                                            API
 --------------                                             -----------
        |                                                      |
        |                   GET /api/employees                 |
        |----------------------------------------------------->|
        |                     403 Forbidden                    |
        |<-----------------------------------------------------|
        |                                                      |
        |                                                      |
        |                 POST /api/authenticate               |
        |     { login: "john.doe", password: "password" }      |
        |----------------------------------------------------->|
        |                      200 Success                     |
        |             { token: "my.personal.token" }           |
        |<-----------------------------------------------------|
        |                                                      |
        |                                                      |
        |                 GET /api/employees                   |
        | Header { "Authorization: Token "my.personal.token" } |
        |----------------------------------------------------->|
        |                      200 Success                     |
        |<-----------------------------------------------------|
        |                                                      |
---------------------

6. Explain and demonstrate a system using jwt's, focusing on both client and server side: 

----------------------

7. Explain and demonstrate use of the npm passportjs module:

-------------------
