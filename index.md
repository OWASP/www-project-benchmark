---

layout: col-sidebar
title: OWASP Benchmark
site_side: true
tags: benchmark
project: true
level: 3
type: tool
pitch: The OWASP Benchmark Project contains language specific test suites designed to evaluate the accuracy, coverage, and speed of automated software vulnerability detection tools.

---


<!-- rebuild 40 -->

[![OWASP Lab](https://img.shields.io/badge/owasp-lab%20project-yellow)](https://www.owasp.org/projects)

## OWASP Benchmark Project

The OWASP Benchmark Project contains test suites in different languages along with scoring tools designed to evaluate the accuracy, coverage, and speed of automated software vulnerability detection tools for different programming languages. Without the ability to measure these tools, it is difficult to understand their strengths and weaknesses, and compare them to each other.

OWASP Benchmark provides multiple fully runnable open source web application that contains thousands of exploitable test cases, each mapped to specific CWEs, which can be analyzed by any type of Application Security Testing (AST) tool, including SAST, DAST (like ZAP), and IAST tools. The intent is that all the vulnerabilities deliberately included in and scored by the Benchmark are actually exploitable so its a fair test for any kind of application vulnerability detection tool. The Benchmark also includes dozens of scorecard generators for numerous open source and commercial AST tools, and the set of supported tools is growing all the time.

## OWASP Benchmark for Java

The initial version 1.0 of the OWASP Benchmark for Java was released in 2015. Version 1.2, which added a full web UI and other improvments was released in 2016 and has been maintained since that without substantial changes to the test cases.

## OWASP Benchmark for Python

The Benchmark Project has just released an initial v0.1 version of a new OWASP Benchmark for Python, which we plan to work on refining and improving to get a v1.0 release out in early 2026.

## Related Projects
* [NSA's Juliet for Java](https://samate.nist.gov/SARD/testsuite.php)
* [The Web Application Vulnerability Scanner Evaluation Project (WAVSEP)](https://sectooladdict.blogspot.com/)
