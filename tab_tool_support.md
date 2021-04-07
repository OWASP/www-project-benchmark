---
title: Tool_Support
displaytext: Tool Support/Results
layout:  null
tab: true
order: 4
tags: benchmark
---

The results, from several years ago, for 5 free tools, PMD, FindBugs, FindBugs with the FindSecBugs plugin, SonarQube and OWASP ZAP are available here against version 1.2 of the Benchmark: [https://rawgit.com/OWASP/Benchmark/master/scorecard/OWASP_Benchmark_Home.html](https://rawgit.com/OWASP/Benchmark/master/scorecard/OWASP_Benchmark_Home.html). We've included multiple versions of FindSecBugs' and ZAP's results so you can see the improvements they are making finding vulnerabilities in Benchmark.

We have Benchmark results for all the following tools, but haven't publicly released the results for any commercial tools. However, we included a 'Commercial Average' page, which includes a summary of results for 6 commercial SAST tools along with anonymous versions of each SAST tool's scorecard.

The Benchmark can generate results for the following tools:

**Free Static Application Security Testing (SAST) Tools:**

* [PMD](https://pmd.github.io/) (which really has no security rules) - .xml results file
* [FindBugs](http://findbugs.sourceforge.net/) - .xml results file (Note: FindBugs hasn't been updated since 2015. Use SpotBugs instead (see below))
* [Semgrep] (https://semgrep.dev/) - .json results file (e.g., semgrep -f https://semgrep.dev/p/r2c-security-audit . --json > results/Benchmark_1.2-Semgrep.json)
* [SonarQube](https://www.sonarqube.org/downloads/) - .xml results file
* [SpotBugs](https://spotbugs.github.io/) - .xml results file. This is the successor to FindBugs.
* SpotBugs with the [FindSecurityBugs plugin](https://find-sec-bugs.github.io/) - .xml results file
* [Visual Code Grepper](https://sourceforge.net/projects/visualcodegrepp/) - [Soure Code here](https://github.com/nccgroup/VCG) - .xml results file

Many of these free SAST tools come bundled with Benchmark so you can run them yourselves. Simply run script/runTOOLNAME.(sh/bat) and it puts the results into the /results directory automatically. There are scripts for running PMD, FindBugs, SpotBugs, and FindSecBugs.

Note: We looked into supporting [Checkstyle](https://checkstyle.sourceforge.io/) but it has no security rules, just like PMD. The [fb-contrib FindBugs plugin](http://fb-contrib.sourceforge.net/) doesn't have any security rules either. We did test [Error Prone](https://errorprone.info/), and found that it does report some use of [insecure ciphers (CWE-327)](https://errorprone.info/bugpattern/InsecureCryptoUsage), but that's it.

**Commercial SAST Tools:**

* [CAST Application Intelligence Platform (AIP)](https://www.castsoftware.com/products/application-intelligence-platform) - .xml results file
* [Checkmarx CxSAST](https://www.checkmarx.com/products/static-application-security-testing) - .xml results file
* [HCL (Formerly IBM) AppScan SAST (Standalone and Cloud)](https://www.hcltechsw.com/wps/portal/products/appscan/home) - .ozasmt or .xml results file
* [Julia Analyzer](https://juliasoft.com) - Acquired by Grammatech. No parser for this new solution yet.
* [Kiuwan Code Security](https://www.kiuwan.com/code-security-sast/) - .threadfix results file
* [Micro Focus (Formerly HPE) Fortify (On-Demand and stand-alone versions)](https://software.microfocus.com/en-us/products/static-code-analysis-sast/overview) - .fpr results file
* [Parasoft Jtest](https://www.parasoft.com/products/jtest/) - .xml results file
* [Semmle LGTM](https://semmle.com/lgtm) - .sarif results file
* [ShiftLeft SAST](https://www.shiftleft.io/product/) - .sl results file (Benchmark specific format. Ask vendor how to generate this)
* [Snappycode Audit's SnappyTick Source Edition (SAST)](https://snappycodeaudit.com/category/static-code-analysis) - .xml results file
* [SourceMeter](https://www.sourcemeter.com) - .txt results file of ALL results from VulnerabilityHunter
* [Synopsys Coverity SAST (Formerly Coverity Code Advisor) (On-Demand and stand-alone versions)](https://www.synopsys.com/software-integrity/security-testing/static-analysis-sast.html) - .json results file (You can scan Benchmark w/Coverity for free. See: https://scan.coverity.com/)
* [Thunderscan SAST](https://www.defensecode.com/thunderscan.php) - .xml results file
* [Veracode SAST](https://www.veracode.com/products/binary-static-analysis-sast) - .xml results file
* [XANITIZER](https://www.xanitizer.com/xanitizer/) - .xml results file ([Their white paper on how to setup Xanitizer to scan Benchmark](https://www.xanitizer.com/wp-content/uploads/howtosetupxanitizerforowaspbenchmarkproject.pdf).) (Free trial available)

We are looking for results for other commercial SAST tools. If you have a license for any static analysis tool not already listed above and can run it on Benchmark and send us the results file that would be very helpful.

If you have a license for any commercial SAST tool, you can also run them against the Benchmark. Just put your results files in the /results folder of the project, and then run createScorecards.sh/.bat and it will generate a scorecard in the /scorecard directory for all the tool results you have that are currently supported.

**Free Dynamic Application Security Testing (DAST) Tools:**

Note: While we support scorecard generators for these Free and Commercial DAST tools, it can be difficult to get a full/clean run against the Benchmark. As such, some of these scorecard generators might need some additional work to properly reflect their results. If you notice any problems, let us know.

* [Arachni](https://www.arachni-scanner.com/) - .xml results file
	* To generate .xml, run: ./bin/arachni_reporter "Your_AFR_Results_Filename.afr" --reporter=xml:outfile=Benchmark1.2-Arachni.xml
* [OWASP ZAP](/www-project-zap/) - .xml results file. To generate a complete ZAP XML results file so you can generate a valid scorecard, make sure you:
	* Tools > Options > Alerts - And set the Max alert instances to like 500.
	* Then: Report > Generate XML Report...
* [Wapiti](https://wapiti.sourceforge.io/) - .xml results file.

**Commercial DAST Tools:**

* [Acunetix Web Vulnerability Scanner (WVS)](https://www.acunetix.com/vulnerability-scanner/) - .xml results file ([see Exporting Scan Results (Generic XML export))](https://www.acunetix.com/resources/wvs11manual.pdf) was the command line /ExportXML switch) or .xml results file from Acunetix 360
* [Burp Pro](https://portswigger.net/burp) - .xml results file
** To generate XML results: click on benchmark in site map so you see ALL findings in Issues pane. Then select ALL issues in Issues pane, right-click and select 'Report selected issues'. Select XML, then next, next, next, and save to file. To reduce size of results file, you can eliminate all the details, and not include requests/responses, which reduces the file size by 2/3rds.
* [HCL (Formerly IBM) AppScan DAST](https://www.hcltechsw.com/wps/portal/products/appscan/home) - .xml results file
* [Micro Focus Fortify WebInspect](https://www.microfocus.com/en-us/products/webinspect-dynamic-analysis-dast/overview) - .xml results file
* [Netsparker](https://www.netsparker.com/web-vulnerability-scanner/) - .xml results file
* [Qualys Web App Scanner](https://www.qualys.com/apps/web-app-scanning/) - .xml results file
* [Rapid7 AppSpider](https://www.rapid7.com/products/appspider/) - .xml results file

If you have access to other DAST Tools, PLEASE RUN THEM FOR US against the Benchmark, and send us the results file so we can build a scorecard generator for that tool.

**Commercial Interactive Application Security Testing (IAST) Tools:**

* [Checkmarx CxIAST](https://www.checkmarx.com/products/interactive-application-security-testing) - .csv results file
* [Contrast Assess](https://www.contrastsecurity.com/interactive-application-security-testing-iast) - .log results file (You can scan Benchmark w/Contrast for free. See: https://www.contrastsecurity.com/contrast-community-edition)
* [Hdiv Detection (IAST)](https://hdivsecurity.com/interactive-application-security-testing-iast) - .hlg results file
* [SecZone VulHunter IAST](https://www.seczone.cn/channels/SDL-IAST.html) - .log results file
** You'll have to ask the vendor how to generate this file.
* [Synopsys Seeker IAST](https://www.synopsys.com/software-integrity/security-testing/interactive-application-security-testing.html) - .csv results file

**Commercial Hybrid Analysis Application Security Testing Tools:**

* [Fusion Lite Insight](https://www.iappsecure.com/products.html) - .xml results file

**WARNING: If you generate results for a commercial tool, be careful who you distribute it to. Each tool has its own license defining when any results it produces can be released/made public. It may be against the terms of a commercial tool's license to publicly release that tool's score against the OWASP Benchmark. The OWASP Benchmark project takes no responsibility if someone else releases such results.**
