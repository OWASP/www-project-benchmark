---
title: Tool_Support
displaytext: Tool Support/Results
layout:  null
tab: true
order: 4
tags: benchmark
---

The results for 5 free tools, PMD, FindBugs, FindBugs with the FindSecBugs plugin, SonarQube and OWASP ZAP are available here against version 1.2 of the Benchmark: https://rawgit.com/OWASP/Benchmark/master/scorecard/OWASP_Benchmark_Home.html. We've included multiple versions of FindSecBugs' and ZAP's results so you can see the improvements they are making finding vulnerabilities in Benchmark.

We have Benchmark results for all the following tools, but haven't publicly released the results for any commercial tools. However, we included a 'Commercial Average' page, which includes a summary of results for 6 commercial SAST tools along with anonymous versions of each SAST tool's scorecard.

The Benchmark can generate results for the following tools:

**Free Static Application Security Testing (SAST) Tools:**

* [PMD](https://pmd.github.io/) (which really has no security rules) - .xml results file
* [FindBugs](http://findbugs.sourceforge.net/) - .xml results file (Note: FindBugs hasn't been updated since 2015. Use SpotBugs instead (see below))
* [SonarQube](https://www.sonarqube.org/downloads/) - .xml results file
* [SpotBugs](https://spotbugs.github.io/) - .xml results file. This is the successor to FindBugs.
* SpotBugs with the [FindSecurityBugs plugin](http://find-sec-bugs.github.io/) - .xml results file

Note: We looked into supporting [Checkstyle](http://checkstyle.sourceforge.net/) but it has no security rules, just like PMD. The [fb-contrib FindBugs plugin](http://fb-contrib.sourceforge.net/) doesn't have any security rules either. We did test [Error Prone](http://errorprone.info/), and found that it does report some use of [insecure ciphers (CWE-327)](http://errorprone.info/bugpattern/InsecureCryptoUsage), but that's it.

**Commercial SAST Tools:**

* [CAST Application Intelligence Platform (AIP)](https://www.castsoftware.com/products/application-intelligence-platform) - .xml results file
* [Checkmarx CxSAST](https://www.checkmarx.com/products/static-application-security-testing/) - .xml results file
* [HCL (Formally IBM) AppScan SAST (Standalone and Cloud)](https://www.hcltechsw.com/wps/portal/products/appscan/home) - .ozasmt or .xml results file
* [Julia Analyzer](https://juliasoft.com/solutions/julia-for-security/) - .xml results file
* [Kiuwan Code Security](https://www.kiuwan.com/code-security-sast/) - .threadfix results file
* [Micro Focus (Formally HPE) Fortify (On-Demand and stand-alone versions)](https://software.microfocus.com/en-us/products/static-code-analysis-sast/overview) - .fpr results file
* [Parasoft Jtest](https://www.parasoft.com/products/jtest/) - .xml results file
* [Semmle LGTM](https://semmle.com/lgtm) - .sarif results file
* [ShiftLeft SAST](https://www.shiftleft.io/product/) - .sl results file (Benchmark specific format. Ask vendor how to generate this)
* [Snappycode Audit's SnappyTick Source Edition (SAST)](https://snappycodeaudit.com/category/static-code-analysis) - .xml results file
* [SourceMeter](https://www.sourcemeter.com/features/) - .txt results file of ALL results from VulnerabilityHunter
* [Synopsys Coverity SAST (Formerly Coverity Code Advisor) (On-Demand and stand-alone versions)](https://www.synopsys.com/software-integrity/security-testing/static-analysis-sast.html) - .json results file (You can scan Benchmark w/Coverity for free. See: https://scan.coverity.com/)
* [Thunderscan SAST](https://www.defensecode.com/thunderscan.php) - .xml results file
* [Veracode SAST](https://www.veracode.com/products/binary-static-analysis-sast) - .xml results file
* [XANITIZER](https://www.rigs-it.com/xanitizer/) - .xml results file ([Their white paper on how to setup Xanitizer to scan Benchmark](https://www.rigs-it.com/wp-content/uploads/2018/03/howtosetupxanitizerforowaspbenchmarkproject.pdf).) (Free trial available)

We are looking for results for other commercial static analysis tools like: [Grammatech CodeSonar](https://www.grammatech.com/products/codesonar), [RogueWave's Klocwork](https://www.roguewave.com/products-services/klocwork), etc. If you have a license for any static analysis tool not already listed above and can run it on the Benchmark and send us the results file that would be very helpful.

The free SAST tools come bundled with the Benchmark so you can run them yourselves. If you have a license for any commercial SAST tool, you can also run them against the Benchmark. Just put your results files in the /results folder of the project, and then run the BenchmarkScore script for your platform (.sh / .bat) and it will generate a scorecard in the /scorecard directory for all the tools you have results for that are currently supported.

**Free Dynamic Application Security Testing (DAST) Tools:**

Note: While we support scorecard generators for these Free and Commercial DAST tools, we haven't been able to get a full/clean run against the Benchmark from most of these tools. As such, some of these scorecard generators might still need some work to properly reflect their results. If you notice any problems, let us know.

* [Arachni](http://www.arachni-scanner.com/) - .xml results file
	* To generate .xml, run: ./bin/arachni_reporter "Your_AFR_Results_Filename.afr" --reporter=xml:outfile=Benchmark1.2-Arachni.xml
* [OWASP ZAP](https://www2.owasp.org/www-project-zap/) - .xml results file. To generate a complete ZAP XML results file so you can generate a valid scorecard, make sure you:
	* Tools > Options > Alerts - And set the Max alert instances to like 500.
	* Then: Report > Generate XML Report...

**Commercial DAST Tools:**

* [Acunetix Web Vulnerability Scanner (WVS)](https://www.acunetix.com/vulnerability-scanner/) - .xml results file ([Generated using command line interface (see Chapter 10.)](https://www.acunetix.com/resources/wvs11manual.pdf) /ExportXML switch)
* [Burp Pro](https://portswigger.net/burp) - .xml results file
* [HCL (Formally IBM) AppScan DAST](https://www.hcltechsw.com/wps/portal/products/appscan/home) - .xml results file
* [Micro Focus (Formally HPE) Fortify WebInspect](https://www.microfocus.com/en-us/products/webinspect-dynamic-analysis-dast/overview) - .xml results file
* [Netsparker](https://www.netsparker.com/web-vulnerability-scanner/) - .xml results file
* [Qualys Web App Scanner](https://www.qualys.com/apps/web-app-scanning/) - .xml results file
* [Rapid7 AppSpider](https://www.rapid7.com/products/appspider/) - .xml results file

If you have access to other DAST Tools, PLEASE RUN THEM FOR US against the Benchmark, and send us the results file so we can build a scorecard generator for that tool.

**Commercial Interactive Application Security Testing (IAST) Tools:**

* [Contrast Assess](https://www.contrastsecurity.com/interactive-application-security-testing-iast) - .zip results file (You can scan Benchmark w/Contrast for free. See: https://www.contrastsecurity.com/contrast-community-edition)
* [Hdiv Detection (IAST)](https://hdivsecurity.com/interactive-application-security-testing-iast) - .hlg results file
* [Synopsys Seeker IAST](https://www.synopsys.com/software-integrity/security-testing/interactive-application-security-testing.html) - .csv results file

**Commercial Hybrid Analysis Application Security Testing Tools:**

* [Fusion Lite Insight](http://www.iappsecure.com/products.html) - .xml results file

**WARNING: If you generate results for a commercial tool, be careful who you distribute it to. Each tool has its own license defining when any results it produces can be released/made public. It may be against the terms of a commercial tool's license to publicly release that tool's score against the OWASP Benchmark. The OWASP Benchmark project takes no responsibility if someone else releases such results.**
