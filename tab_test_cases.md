---
title: Test Cases
layout:  null
tab: true
order: 1
tags: benchmark
---

## Summary ##

Version 1.2 and forward of the Benchmark is a fully executable web application, which means it is scannable by any kind of vulnerability detection tool. v1.2 has been limited to slightly less than 3,000 test cases, to make it easier for DAST tools to scan it (so it doesn't take so long and they don't run out of memory, or blow up the size of their database). The 1.2 release covers the same vulnerability areas that 1.1 covers. The bulk of the work was turning each test case into something that actually runs correctly and is fully exploitable, and then generating a UI on top that works in order to turn the test cases into a real running application.

The test case areas and quantities for the Benchmark releases are:

Vulnerability Area | # of Tests in v1.1 | # of Tests in v1.2 | CWE Number
------------------ | ------------------ | ------------------ | ----------
Command Injection | 2708 | 251 | 78
Weak Cryptography | 1440 | 246 | 327
Weak Hashing | 1421 | 236 | 328
LDAP Injection | 736 | 59 | 90
Path Traversal | 2630 | 268 | 22
Secure Cookie Flag | 416 | 67 | 614
SQL Injection | 3529 | 504 | 89
Trust Boundary Violation | 725 | 126 | 501
Weak Randomness | 3640 | 493 | 330
XPATH Injection | 347 | 35 | 643
XSS (Cross-Site Scripting) | 3449 | 455 | 79
**Total Test Cases** | **21,041** | **2,740**

Each Benchmark version comes with a spreadsheet that lists every test case, the vulnerability category, the CWE number, and the expected result (true finding/false positive). Look for the file: expectedresults-VERSION#.csv in the project root directory.

Every test case is:

* an HTTP Servlet
* a true vulnerability or a false positive for a single CWE

## Release History ##
* Version 1.0 of the Benchmark was released April 15, 2015 and had 20,983 test cases.
* Version 1.1 of the Benchmark was released May 23, 2015. The 1.1 release improved on the previous version by making sure that there are both true positives and false positives in every vulnerability area.
* Version 1.2 was first released on June 5, 2016 (The 1.2beta was August 15, 2015). There have been constant tweaks to the v1.2 release since then.

## Potential future enhancements: ##

* All vulnerability types in the OWASP Top 10
* Does the tool find flaws in libraries?
* Does the tool find flaws spanning custom code and libraries?
* Does tool handle web services? REST, XML, GWT, etc…
* Does tool work with different app servers? Java platforms?
* JSPs
* More popular frameworks
* Inversion of control
* Reflection
* Class loading
* Annotations
* Popular UI technologies (e.g., JavaScript frameworks)
* Entirely new languages (C#, Python, etc.)

## Example Test Case ##

Each test case is a simple Java EE servlet. BenchmarkTest00001 in version 1.0 of the Benchmark was an LDAP Injection test with the following metadata in the accompanying BenchmarkTest00001.xml file:

```xml
 <test-metadata>
   <category>ldapi</category>
   <test-number>00001</test-number>
   <vulnerability>true</vulnerability>
   <cwe>90</cwe>
 </test-metadata>
```

BenchmarkTest00001.java in the OWASP Benchmark 1.0 simply reads in all the cookie values, looks for a cookie named "foo", and uses the value of this cookie when performing an LDAP query. Here's the code for BenchmarkTest00001.java:

```java
 package org.owasp.benchmark.testcode;
 
 import java.io.IOException;
 
 import javax.servlet.ServletException;
 import javax.servlet.annotation.WebServlet;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 
 @WebServlet("/BenchmarkTest00001")
 public class BenchmarkTest00001 extends HttpServlet {
 	
 	private static final long serialVersionUID = 1L;
 	
 	@Override
 	public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
 		doPost(request, response);
 	}
 
 	@Override
 	public void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
 		// some code
 
 		javax.servlet.http.Cookie[] cookies = request.getCookies();
 		
 		String param = null;
 		boolean foundit = false;
 		if (cookies != null) {
 			for (javax.servlet.http.Cookie cookie : cookies) {
 				if (cookie.getName().equals("foo")) {
 					param = cookie.getValue();
 					foundit = true;
 				}
 			}
 			if (!foundit) {
 				// no cookie found in collection
 				param = "";
 			}
 		} else {
 			// no cookies
 			param = "";
 		}
 		
 		try {
 			javax.naming.directory.DirContext dc = org.owasp.benchmark.helpers.Utils.getDirContext();
 			Object[] filterArgs = {"a","b"};
 			dc.search("name", param, filterArgs, new javax.naming.directory.SearchControls());
 		} catch (javax.naming.NamingException e) {
 			throw new ServletException(e);
 		}
 	}
 }
 ```
 