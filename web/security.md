# Notes from penn state spring 2020/insc_561 class

Q: HTTP Proxy
A: Proxies sit between your client and the server the client is talking to.
Example: `nginx` reverse proxy
WebGoat application
<!-- 1548852468371 -->

Q: Authentication Technologies
A: HTML forms-based authentication (most common)
Multifactor mechanisms, combines passwords and physical devices (super safe)
Client SSL certificates and/or smartcards (much overhead)
HTTP basic and digest authentication (rarely used)
Windows integrated using: NTML or Kerberos (rarely used)
Chapter 6, page 160
<!-- 1549025373713 -->

Q: What is Q: JSON Web Token
A: Open Standard (RFC 7519)
Securely transfer information between two bodies
Digitally signed. Secure, verified and trusted.
Fast, compact.
Used in web authentication.
Composed: header, payload, signature
One Time database query. <br><img src="jwt.png">
<!-- 1549136365749 -->

Q: Chapter9::Attacking Data Stores::What is a data store?
A: They hold data in a structured way.
Data is accessed by a query format or language
Contain internal logic to help manage the data

Q: Chapter9::Attacking Data Stores::What is code injection?
A: Database languages are not compiled, they use an interpreter
Code executed in the database is a mix of the programmer's code and user input
Here is where the hacker can craft an input that breaks out the programmer's desired context

Q: Chapter9::Attacking Data Stores::Login Bypass Query 1/2
A: Database languages are not compiled, they use an interpreter
Code executed in the database is a mix of the programmer's code and user input
Here is where the hacker can craft an input that breaks out the programmer's desired context
