---
title: Python_Test_Cases
displaytext: Python Test Cases
layout:  null
tab: true
order: 2
tags: benchmark
---

## Summary ##

Version 0.1 of the OWASP Benchmark for Python is a fully executable web application, which means it is scannable by any kind of vulnerability detection tool. v0.1 is a preliminary release that we plan to refine and improve over the next few months to get to a full v1.0 release that is similar to the level of completeness of the OWASP Benchmark for Java v1.2.
 
The test case areas and quantities for the initial OWASP Benchmark for Python v0.1 are:

Vulnerability Area | # of Tests in v0.1 | CWE Number
------------------ | ------------------ | ----------
Code Injection | 61 | 94
Command Injection | 22 | 78
Deserialization of Untrusted Data | 55 | 502
LDAP Injection | 21 | 90
Path Traversal | 156 | 22
Secure Cookie Flag | 37  | 614
SQL Injection | 34 | 89
Trust Boundary Violation | 33 | 501
Unchecked Redirects | 42 | 601
Weak Hashing | 156 |  328
Weak Randomness | 321 | 330
XPath Injection | 180 | 643
XSS (Cross-Site Scripting) | 100 | 79
XXE (Xml eXternal Entity Injection) | 25 | 611
**Total Test Cases** | **1,243**

FUTURE WORK:

Other CWEs we might add:
Weak Cryptography | 327
Regex DOS | 1333

We will also likely work on trying to balance the number of true positives and false positives per test case category to be more even.


Each Benchmark version comes with an expected results spreadsheet that lists every test case, the vulnerability category, the CWE number, and the expected result (true finding/false positive). Look for the file: expectedresults-VERSION#.csv in the project root directory.

Every test case is:

* a single web page and web endpoint
* a true vulnerability or a false positive for a single CWE

The structure and organization of the Benchmark for Python is very similar to the OWASP Benchmark for Java v1.2.

## REQUESTS ##

Please provide us with feedback on any suggested fixes/improvements/bugs or tools you'd like to us to add scanning support for. As well as CWEs or Popular Python frameworks we should add test cases for.

## Acknowledgements ##
The OWASP Benchmark project would like to thank the contributions of AppSecAI (https://www.appsecai.io) and their team members Theo Cartsonis and Jessica Salawu for doing the bulk of the development work to produce this first release of the Benchmark for Python test suite.

