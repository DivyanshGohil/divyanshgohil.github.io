---
title: 'Hacking Web Application'
date: 2025-07-09
permalink: /posts/2025/07/web-vulnerabilities/
tags:
  - VAPT
  - Digital Security
  - Web Security
---

## Introduction to Web Application

Web applications are software programs that run on web browsers and act as the interface between users and web servers through web pages.

On receiving the request, the web server checks the file extension:

1.  If the user requests a simple web page with a HTM or HTML extension, the web server processes the request and sends the file to the user's browswer.
    
2.  If the user requests a web page with extension that needs to be processed at the server side, such as php, asp, and cfm then the web application server must process the request.

## Vulnerability Stack

<div style="text-align:center"><img src="/images/hacking1.jpg" /></div><br>


## Owasp Top 10 Application Security Risk - 2021

OWASP (Open Worldwide Application Security Project) is an international organization that maintains a list of the top 10 vulnerabilities and flaws of web applications.

**A01 - Broken Access Control**

This vulnerability is related to improperly enforced restriction on the action of authenticated users.

Attacker can exploit these flaws to access unauthorized functionality and data such as access to other user accounts, viewing of sensitive files, modifications to other user data, and changes to access rights.

**A02 - Cryptographic Failures**

Mostly web application and APIs do not properly protect sensitive data such as financial data, healthcare data and personally identifiable information (PII).

Moreover, many application developers fail to implement strong cryptographic keys, use old keys or fail to enforce proper key management. In such case sensitive data can be transmitted in cleartext through HTTP.

**A03 - Injection**

Injection flaws, such as SQL injection and LDAP injection occurs when untrusted data are send to an interpreter as part of command or query. This data can trick the interpreter into executing unintended commands or accessing data without proper authorization

SQL Injection involves the injection of malicious sql queries into user input forms.

Command Injection involves the injection of malicious code through a web application

LDAP Injection involves the injection of malicious LDAP statements.

XSS involves the injection and execution of malicious scripts in the web browser.

**A04 - Insecure Design**

During application development, if security controls are not properly implemented considering the latest business risks, various design flaws may occurs.

These design flaws can compromise the integrity, confidentiality and authenticity of data.

Attacker can use these flaws to perform session hijacking, credential theft, spoofing, and other types of MITM attacks.

**A05 - Security Misconfiguration**

Security Misconfiguration is the most common issue in web security, which is due to manual  or ad hoc configuration, insecure default configurations, open S3 buckets, misconfigure HTTP headers, error message containing sensitive information and failure to patch or upgrade systems, frameworks, dependencies and components in a timely manner.

**A06 - Vulnerable and Outdated Components**

Components such as libraries, frameworks, and other software modules run with the same privileges as the application.

As they become outdated which can leave serious vulnerabilities. An attack exploiting a vulnerable component can cause serious data loss or server takeover.

The software components need to be updated or patched in a timely manner based on the current risks.

**A07-Identification and Authentication Failures**

Application functions related to identification, authentication and session management are often implemented incorrectly.

Allowing attackers to launch brute forcing, password spraying, and other automated attacks to compromise passwords, keys or session tokens.

**A08 - Software and Data Integrity Failures**

Many applications are implemented with auto update features. Such applications may download updates from unauthorized or previously trusted sources without conducting sufficient integrity checks.

Attackers can take advantage of this flaw and load their own updates to distribute malware

If data are encoded or serialized into an easily understandable format, attackers can alter the data, leading to an insecure deserialization flaw.

**A09 - Security Logging and Monitoring Failures**

Security logging and monitoring failures occurs via insufficient log monitoring, the local storage of logs, inadequate error message, inappropriate alert mechanisms for failed login attempts, or applications failing to identify threats in advance

Such vulnerabilities can leak sensitive information that can be leveraged by the attackers to compromise a system or account, tamper with credentials, or destroy data.

**A10 - Server Side Request Forgery (SSRF)** 

SSRF is a web security vulnerability that arises when remote resources are obtained by an application without verifying the URL entered by the user.

Attackers can use this vulnerability to abuse the functionality of server to read and modify internal resources and steal sensitive information by sending malicious requests.

Attackers exploit SSRF vulnerabilities in a public web server to send crafted requests to the internal or backend servers.

SSRF vulnerabilities also allow attackers to send malicious requests to internal systems, even if they are secured by firewalls.

## Web Vulnerabilities

**SQL Injection**

SQL Injection is a technique used to take advantage of unsanitized input vulnerabilities to pass SQL commands through a web application for execution by a backend database.

SQL Injection is a basic attack used to either gain unauthorized access to a database or retrieve information directly from the database.

It is a flaw in web applications and not a database or web server issue.

SQL injection can be used to implement the following types of attacks:

1.  Authentication and Authorization Bypass
2.  Compromised integrity and Availability of Data
3.  Information Disclosure
4.  Remote Code Execution

There are three main types of SQL injection:

**In-Band SQL Injection**: An attacker uses the same communication channel to perform the attack and retrieve the results. The commond used in-band SQL injection attacks are error-based SQL injection and UNION SQL injection.

**Blind SQL Injection**: In Blind injection, the attacker has no error messages from the system to work on. Instead, the attacker simply sends a malicious SQL query to the database. This type of SQL injection takes a longer time to execute. Mainly there are Time Delay and Boolean Exploitation.

**Out-of-Band SQL Injection**: Attackers use different communication channels such as databse email functionality or file writing and loading functionality to perform the attack and obtain the results

**MongoDB / NoSQL Injection Attack**

Attackers use MongoDB operations such as $eq (equal), $ne (not equal to), $gt (greater than) $gte (greater than or equal to) and $regex to create a malicious command that bypasses the authentication procedure

**Remediation of SQL Injection**

Implement multiple layers of validation and never concatenate user input that is not validated.

Apply the least privilege rule to run the applications that access the DBMS.

Ensure that all user inputs are sanitized before using them in dynamic SQL statements.

**Command Injection Attacks**

**Shell Injection**

An attacker tries to craft an input string to gain shell access to a web server.

**HTML Embedding**

This type of attack is used to deface websites virtually. Using this attack, an attacker adds extra HTML-based content to the vulnerable web application

**File Injection**

The attacker exploits this vulnerability and injects malicious code into system files.

File injection attacks enable attackers to exploit vulnerable scripts on the server to use a remote file.

**Remediation of File Injection**

Strongly validate user input.

PHP: Disable allow\_url\_fopen and allow\_url\_include in php.ini

**LDAP Injection**

LDAP  Directory Services store and organize information based on its attributes. The information is hierarchically organized as a tree of directory entries.

LDAP injection attacks are similar to SQL Injection attacks, but exploit user parameters to generate an LDAP query.

LDAP injection techniques take advantage of non-validated web application input vulnerabilities and pass LDAP filters used for searching Directory services to obtain direct access to databases behind the LDAP tree.

**Remediation of LDAP Injection**

Perform type, pattern and domain value validation on all input data.

Make the LDAP filter as specific as possible.

Validate and restrict the amount of data returned to the user.

Implement proper access control on the data in the LDAP directory.

Use LDAPS (LDAP over SSL) to secure communication on the web server.

**Server-Side JS Injection**

Vulnerabilities for Server-Side Javascript injection emerge when an application integrates user-controllable values into a string that is dynamically validated by a code interpreter.

**Server-Side Includes Injection**

Server-Side Includes is an application feature that helps designers to auto generate the content of web page without manual involvement

Attacker exploit this feature to pass malicious directives as input values and perform malicious activities.

**Server-Side Template Injection**

Server-side template injection occurs when users are allowed to insert unsafe inputs into a server-side template

Attacker can inject malicious template directives to run arbitrary code and gain complete control over the target web server.

**Log Injection**

Attacker launch log injection attacks by exploiting the acceptance of unsanitized or non-validated input into application logs.

**HTML Injection**

Attackers exploit vulnerable form inputs to inject HTML code into web page and change the appearance of the website or the information provided to its users.

**Remediation of HTML Injection**

Validate all the users inputs to remove the HTML-syntax substrings from user-supplied text

Check the input for unwanted script or HTML code such as <script></script>,<html></html>

Enable the HttpOnly flag on the server side to ensure that all cookies generated by the application are not available to the client user.

**CRLF Injection**

Attackers inject carriage return ( \\r ) and linefeed ( \\n ) characters into user input to trick a web server, web application, or user into terminating the input of a current object and initiate a new object.

**Remediation of CRLF Injection**

Use any function to encode CRLF special characters and avoid using the user input in the response headers.

Update the version of programming language that disallows the injection of CR and LF characters.

Encrypt the data that is passed to the HTTP headers to hide the CR and LF codes

**Cross-Site Scripting (XSS)**

XSS attack exploit vulnerabilities in dynamically generated web pages, which enables malicious attackers to inject client side scripts into web pages viewed by other users

Some exploitation that can be performed by XSS attacks are as follows:

*   Malicious Script Execution
*   Redirecting to a malicious server
*   Exploiting user privileges
*   Ads in hidden iframes and pop-ups
*   Data manipulation
*   Session Hijacking
*   Data theft
*   Intranet probing
*   Keylogging and remote monitoring

**Remediation of XSS**

Validate all headers, cookies, query strings, form fields, and hidden fields against all rigorous specification.

Use the application firewall to block the execution of malicious script.

Convert all non-alphanumeric characters to HTML character entities before displaying the user input in search engines and forums.

Encode input and output and filter meta characters in the input.

**XML External Entity (XXE)**

XML(Extensible Markup Language) External Entity attack is a server-side request forgery (SSRF) attack that can occur when a misconfigured XML parser allows applications to parse XML input from an unreliable source.

Attackers can refer a victim's web application to an external entity by including the reference in the malicious XML input

when this malicious input is processed by the weakly configured XML parser of a target web application, it enables the attacker to access protected files and services from servers or connected networks

**Remediation of XXE**

Avoid processing XML input containing a reference to an external entity by a weakly configure XML parser.

Parse the document with a securely configured parser

**Insecure Deserialization**

As data in the computer is stored in the form of data structures, Data serialization and deserialization is effective process of linearizing and delinearizing data objects for transmission to other networks or systems.

Attackers inject malicious code into serialized data and forward the malicious serialized data to the victim.

Insecure deserialization deserializes the malicious serialized content along with the injected malicious code compromising the system or network.

**Directory Traversal**

Directory traversal allows attackers to access restricted directories, including application source code, configuration, and critical system files to execute commands outside the web server's root application directory.

Attackers can manipulate variables that references file with “dot-dot-slash” (../../../) sequences and its variations.

Accessing files located outside web publishing directory using directory traversal.

**Redirection Attacks**

1.  **Open Redirection**: Open redirection is a vulnerability that allows attacker to add their own parameters to a URL to redirect users from trusted websites to malicious sites.
2.  **Header-Based Open Redirection**: It is process of modifying the HTTP location header to redirect users to a malicious page without their knowledge.
3.  **Javascript-Based Open Redirection**: It is process of injecting Javascript into a web page and this script will redirect the page to malicious sites.

**Watering Hole Attack**

Attackers identifies the kinds of websites which are frequently surfs by users.

When the attackers identifies vulnerabilities in the website, the attacker inject malicious script/code into the web application that can redirect the webpage and download malware onto the victim machine.

This attack is called a watering hole attack because the attacker waits for the victim to fall into a trap, similar to a lion waiting for its prey to arrive at a watering hole to drink water.

**Cross-Site Request Forgery (CSRF) Attack**

Cross-Site Request Forgery (CSRF) attacks exploit web page vulnerabilities that allows an attacker to force an user's browser to send malicious requests they did not intend.

The victim holds an active session with trusted site and simultaneously visits a malicious site, which injects an HTTP request for the trusted site into the victim user's session, compromising its integrity.

<div style="text-align:center"><img src="/images/hacking2.jpg" /></div><br>

**Cookie/Session Poisoning**

Cookies are generally used to maintain a session between web application and users. The attacker can modify the cookies information with ease to escalate access or assume the identity of another user. Possible attack are,

1.  **Modify the Cookie content:** Modifying the contents of a cookie (personal information stored in web user's computer) to bypass security mechanisms.
2.  **Inject the Malicious Content**: This allows an attacker to inject malicious content, modify the user's online experience, and obtain unauthorized information.
3.  **Rewriting the session data**: A proxy can be used for rewriting the session data, displaying the cookie data, and specifying a new user ID or other session identifiers int he cookie.
    

**Web-based Timing Attacks**

A web-based timing attack is a type of side-channel attack performed by attackers to retrieve sensitive information such as passwords from web applications by measuring the response time taken by the server.

1.  **Direct Timing Attack**: Direct timing attacks are carried out by measuring the approximate time taken by the server to process a POST request to deduce the existence of  a username.
2.  **Cross-site Timing Attack**: A cross-site timing attack is another type of timing attack, in which attackers send crafted request packets to the website using javascript.
3.  **Browser-based Timing attack:** Attackers take advantage of side channel leaks of a browser to estimate the time taken by the browser to process the requested resources

**Clickjacking Attack**

Attackers perform clickjacking attacks by tricking the victim into clicking on any malicious web page element that is placed transparently on the top of any trusted web page.

Attackers performs this attacks by exploiting the vulnerabilities caused by HTML iframes or improper configuration of the X-Frame-Options header

**DNS Rebinding Attack**

Attackers use the DNS rebinding technique to bypass the Same Origin Policy's security constraints, allowing the malicious web page to communicate or make arbitrary requests to local network or domain.

An attacker creates a malicious website with the domain name xyz.com and registers it with the DNS server controller by attacker. Now, the attacker configures the DNS server to send DNS responses with very short TTL values to avoid caching of the response.

When the victim opens the malicious website, the attacker's DNS server sends the IP address of the HTTP server that hosts the attacker-controlled website http://xyz.com.

The web server response with a page that runs javascript code in the victim's browser.

This javascript make connection with internal resources or server. which will send response to attacker server. 

**Remediation of DNS Rebinding**

Restrict the running of javascript so that attackers can't force requests.

Implement HTTPS communication on all private services. Since HTTPS handshake requires the correct domain to validate the SSL certificate, the attacking scripts won't be able to establish ssl connections to target service during a rebinding attack.

**Same Site Attack**

Same Site attacks also known as related domain attacks, occur when an attacker target the subdomain of the trusted organization and attempts to redirect users to an attacker-controlled web page.

In a same site attack, the attacker redirects a user attempting to browser [www.xyz.com](https://www.xyz.com) to an attacker-controlled dangling site, [www.attack.xyz.com](https://www.attack.xyz.com) . The malicious link shares a common domain name, which lures the user into believing that the redirected site is the secure or legitimate one.

**Pass the Cookie Attack**

Pass the cookie attacks allow attackers to access a user's web services without providing any identity or performing multi-factor authentication.

The pass the cookie attack occurs when attackers obtain a clone of a cookie form the user's browser and uses the cookie to established a session with the target web server.

**HTTP Request Smuggling**

HTTP Request Smuggling is a web application vulnerability that occurs when an attacker manipulates how front-end and back-end servers parse HTTP request. This desynchronization can allow attackers to bypass security controls, smuggle malicious request through trusted channel.

HTTP smuggling happens when there are inconsistencies between the way two servers usually a front end proxy or load balancer and a back end application server parse the same HTTP request.

Request smuggling is primarily associated with HTTP/1 requests. However, websites that support HTTP/2 may be vulnerable, depending on their back-end architecture.

Most commonly, it involves the use of two conflicting headers that indicate the size of the request body:

Content-Length: Specifies the exact byte length of the body.

Transfer-Encoding: chunked : Indicates that the body is sent in chunks.

<div style="text-align:center"><img src="/images/hacking3.png" /></div><br>

**Mitigate the HTTP Request Smuggling**

Avoid using both Content-Length and Transfer-Encoding headers together.

Implement WAF rules specifically designed to detect request smuggling patterns.

Use updated web servers and proxies, newer versions have better parsing rules.

**Web Cache Deception**

Web cache deception is a web security vulnerability where an attacker tricks a web cache into storing sensitive user-specific data in a public cache, making it accessible to anyone.

Web caches are designed to improve performance by storing copies of static resources like images, CSS, JS files. These are safe to cache because they are same for every user

Example: 

A legitimate URL that shows private data: [https://example.com/account](https://example.com/account)

But the attacker tricks the cache with a modified URL like: [https://example.com/account/style.css](https://example.com/account/style.css)

**Remediation of Web Cache Deception**

Clearly specify which content should be cached. This involves setting up clear caching rules within your application.

Implement strong cache management by using Cache-Control headers. For dynamic content, use settings like no-cache to prevent it from being stored.

Cache-Control: no-store, private

Treat all content as non-cacheable unless it has been explicitly approved for caching. This approach helps minimize the risk of inadvertently caching sensitive information.

**Session Fixation**

Session fixation is an attack that permits an attacker to hijack a valid user session.

This attack is possible due to flaw in web application session management. When authenticating a user, it doesn't assign a new session ID.

In this attack first attacker generate valid session token and inducing a victim to authenticate himself with that session ID.

Now the attacker can use this Session token to execute malicious task as being a authenticated user.

There are several techniques to execute the attack, it depends on how the web application deals with session tokens. Below are the some of the most common technique:

1.  Session token in URL argument
2.  Session token in hidden form field
3.  Session ID in cookie

**IDOR**

Insecure direct object reference (IDOR) is a vulnerability that arises when an application uses user-supplied input to access object directly such as database keys, directories, and other files, that can be exploited by an attacker to modify the references and gain unauthorized access to data

For example, consider this normal request: api.xyz.com/profile/user_id=21

Attacker can manipulate this user_id parameter to gain unauthorized access. The attacker manipulates the above request using parameter pollution also to bypass IDOR. For ex, api.xyz.com/profile/user_id=21&user_id=1