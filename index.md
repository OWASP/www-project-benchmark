---

layout: col-sidebar
title: OWASP Benchmark
site_side: true
tags: benchmark
project: true
level: 3
type: tool
pitch: The OWASP Benchmark Project is a Java test suite designed to evaluate the accuracy, coverage, and speed of automated software vulnerability detection tools.

---
<!-- rebuild 40 -->

[![OWASP Lab](https://img.shields.io/badge/owasp-lab%20project-yellow)](https://www2.owasp.org/projects#div-lab)

## OWASP Benchmark Project

The OWASP Benchmark Project is a Java test suite designed to evaluate the accuracy, coverage, and speed of automated software vulnerability detection tools. Without the ability to measure these tools, it is difficult to understand their strengths and weaknesses, and compare them to each other.

OWASP Benchmark is a fully runnable open source web application that contains thousands of exploitable test cases, each mapped to specific CWEs, which can be analyzed by any type of Application Security Testing (AST) tool, including SAST, DAST (like OWASP ZAP), and IAST tools. The intent is that all the vulnerabilities deliberately included in and scored by the Benchmark are actually exploitable so its a fair test for any kind of application vulnerability detection tool. The Benchmark also includes dozens of scorecard generators for numerous open source and commercial AST tools, and the set of supported tools is growing all the time.

## Related Projects
* [NSA's Juliet for Java](https://samate.nist.gov/SARD/testsuite.php)
* [The Web Application Vulnerability Scanner Evaluation Project (WAVSEP)](https://sectooladdict.blogspot.com/)
