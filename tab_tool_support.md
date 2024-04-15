---
title: Tool_Support
displaytext: Tool Support/Results
layout:  null
tab: true
order: 4
tags: benchmark
---

The results, from several years ago, for 5 free tools, PMD, FindBugs, FindBugs with the FindSecBugs plugin, SonarQube, and ZAP are available here against version 1.2 of the Benchmark: https://github.com/OWASP-Benchmark/BenchmarkJava/blob/master/scorecard/OWASP_Benchmark_Home.html. You'll have to clone this Git repo and open the file locally. We included multiple versions of FindSecBugs' and ZAP's results so you can see the improvements they made finding vulnerabilities in Benchmark.

We have Benchmark results for all the following tools, but haven't publicly released the results for any commercial tools. However, we included a 'Commercial Average' page, which includes a summary of results for 6 commercial SAST tools in 2016 along with anonymous versions of each SAST tool's scorecard.

The Benchmark can generate results for the following tools:

**Free Static Application Security Testing (SAST) Tools (Both Open Source and Commercial):**

* [CodeQL](https://codeql.github.com/) - .sarif results file
* [Contrast CodeSec - Scan](https://www.contrastsecurity.com/developer/codesec/) - .json SARIF format results file
* [FindBugs](http://findbugs.sourceforge.net/) - .xml results file
	* Note: FindBugs hasn't been updated since 2015. Use SpotBugs instead (see below)
* [Horusec](https://github.com/ZupIT/horusec) - .json results file
* [Insider](https://github.com/insidersec/insider) - .json results file
* [PMD](https://pmd.github.io/) (which really has no security rules) - .xml results file
* [Semgrep Code](https://semgrep.dev/) - .sarif results file (.json format supported too)
	* e.g., semgrep -f https://semgrep.dev/p/r2c-security-audit . --sarif > results/Benchmark_1.2-Semgrep.sarif
* [ShiftLeft Scan](https://github.com/ShiftLeftSecurity/sast-scan) - .json results file (found at reports/scan-full-report.json)
* [Snyk Code](https://snyk.io/platform/snyk-cli/) - .sarif results file (note: --json produces the same sarif file)
	* e.g., snyk code test --sarif-file-output=results/Benchmark_1.2-Snyk.sarif
* [SonarQube Community Edition](https://www.sonarqube.org/downloads/) - .xml results file
* [SpotBugs](https://spotbugs.github.io/) - .xml results file. This is the successor to FindBugs.
* SpotBugs with the [FindSecurityBugs plugin](https://find-sec-bugs.github.io/) - .xml results file
* [Visual Code Grepper](https://sourceforge.net/projects/visualcodegrepp/) - [Soure Code here](https://github.com/nccgroup/VCG) - .xml results file

Many of the free Open Source SAST tools come bundled with Benchmark so you can run them yourselves. Simply run script/runTOOLNAME.(sh/bat) and it puts the results into the /results directory automatically. There are scripts for running PMD, FindBugs, SpotBugs, and FindSecBugs.

Note: We looked into supporting [Checkstyle](https://checkstyle.sourceforge.io/) but it has no security rules, just like PMD. The [fb-contrib FindBugs plugin](http://fb-contrib.sourceforge.net/) doesn't have any security rules either. We did test [Error Prone](https://errorprone.info/), and found that it does report some use of [insecure ciphers (CWE-327)](https://errorprone.info/bugpattern/InsecureCryptoUsage), but that's it.

**Commercial (non-Free) SAST Tools:**

* [CAST Application Intelligence Platform (AIP), which is a component of CAST Imaging](https://doc.castsoftware.com/display/IMAGING/CAST+Imaging) - .xml results file
* [Checkmarx SAST](https://checkmarx.com/cxsast-source-code-scanning/) - .xml results file
* [Contrast Scan](https://www.contrastsecurity.com/contrast-scan) - .json SARIF format results file
* [HCL AppScan Source (Standalone and Cloud)](https://www.hcltechsw.com/appscan/offerings/source) - .xml (or legacy .ozasmt) results file
* [Julia Analyzer](https://juliasoft.com) - Acquired by Grammatech. No parser for this new solution yet.
* [Kiuwan SAST](https://www.kiuwan.com/code-security-sast/) - .threadfix results file
* [Mend SAST](https://www.mend.io/sast/) - Formerly WhiteSource and before that XANITIZER - .xml results file
* [Micro Focus Fortify (On-Demand and stand-alone versions)](https://www.microfocus.com/en-us/cyberres/application-security/static-code-analyzer) - .fpr results file
* [Parasoft Jtest](https://www.parasoft.com/products/parasoft-jtest/) - .xml results file
* [Semmle LGTM](https://semmle.com/lgtm) - .sarif results file
* [Qwiet Next Gen SAST (Was ShiftLeft SAST)](https://qwiet.ai/sast/) - .sl results file (Benchmark specific format. Ask vendor how to generate this.)
* [SnappyTick Source Edition (SAST)](https://snappycodeaudit.com/category/static-code-analysis-tools) - .xml results file
* [SonarQube Developer Edition (or greater)](https://www.sonarsource.com/products/sonarqube/downloads/) - .xml results file (same format as Free version)
* [SourceMeter](https://www.sourcemeter.com) - .txt results file of ALL results from VulnerabilityHunter
* [Synopsys Coverity SAST (On-Demand and stand-alone versions)](https://www.synopsys.com/software-integrity/security-testing/static-analysis-sast.html) - .json results file (You can scan Benchmark w/Coverity for free. See: https://scan.coverity.com/)
* [Veracode SAST](https://www.veracode.com/products/binary-static-analysis-sast) - .xml results file

We are looking for results for other commercial SAST tools. If you have a license for any static analysis tool not already listed above and can run it on Benchmark and send us the results file that would be very helpful.

If you have a license for any commercial SAST tool, you can also run them against the Benchmark. Just put your results files in the /results folder of the project, and then run createScorecards.sh/.bat and it will generate a scorecard in the /scorecard directory for all the tool results you have that are currently supported.

**Free Dynamic Application Security Testing (DAST) Tools (Both Open Source and Commercial):**

Note: While we support scorecard generators for these Free and Commercial DAST tools, it can be difficult to get a full/clean run against the Benchmark. As such, some of these scorecard generators might need some additional work to properly reflect their results. If you notice any problems, let us know.

* [Arachni](https://www.arachni-scanner.com/) - .xml results file
	* To generate .xml, run: ./bin/arachni_reporter "Your_AFR_Results_Filename.afr" --reporter=xml:outfile=Benchmark1.2-Arachni.xml
* [Burp Suite Community Edition](https://portswigger.net/burp/communitydownload) - .xml results file
        * To generate XML results: click on benchmark in site map so you see ALL findings in Issues pane. Then select ALL issues in Issues pane, right-click and select 'Report selected issues'. Select XML, then next, next, next, and save to file. To reduce size of results file, you can eliminate all the details, and not include requests/responses, which reduces the file size by 2/3rds.
* [ZAP](https://www.zaproxy.org/) - .json or .xml results file. To generate a complete ZAP results file so you can generate a valid scorecard, make sure you:
	* Tools > Options > Alerts - And set the Max alert instances to like 500.
	* Then: Report > Generate XML Report...
* [Wapiti](https://wapiti.sourceforge.io/) - .json or .xml results file.

**Commercial (non-Free) DAST Tools:**

* [Acunetix Web Vulnerability Scanner (WVS)](https://www.acunetix.com/vulnerability-scanner/) - .xml results file ([see Exporting Scan Results (Generic XML export))](https://www.acunetix.com/resources/wvs11manual.pdf) was the command line /ExportXML switch) or .xml results file from Acunetix 360
* [Burp Suite Pro](https://portswigger.net/burp/pro) - .xml results file
	* To generate XML results: click on benchmark in site map so you see ALL findings in Issues pane. Then select ALL issues in Issues pane, right-click and select 'Report selected issues'. Select XML, then next, next, next, and save to file. To reduce size of results file, you can eliminate all the details, and not include requests/responses, which reduces the file size by 2/3rds.
* [Fluid Attacks DAST](https://fluidattacks.com) - .csv results file
* [HCL AppScan Standard](https://www.hcltechsw.com/appscan/offerings/standard) - .xml results file
* [Micro Focus Fortify WebInspect](https://www.microfocus.com/en-us/products/webinspect-dynamic-analysis-dast/overview) - .xml results file
* [Netsparker](https://www.netsparker.com/web-vulnerability-scanner/) - .xml results file
* [Qualys Web App Scanner](https://www.qualys.com/apps/web-app-scanning/) - .xml results file
* [Rapid7 AppSpider](https://www.rapid7.com/products/appspider/) - .xml results file

If you have access to other DAST Tools, PLEASE RUN THEM FOR US against the Benchmark, and send us the results file so we can build a scorecard generator for that tool.

**Commercial Interactive Application Security Testing (IAST) Tools:**

* [Checkmarx CxIAST](https://www.checkmarx.com/products/interactive-application-security-testing) - .csv results file
* [Contrast Assess](https://www.contrastsecurity.com/contrast-assess) - .log results file
	* You can scan Benchmark w/Contrast Assess for free. See: [https://www.contrastsecurity.com/contrast-community-edition](https://www.contrastsecurity.com/contrast-community-edition)
* [Datadog Application Vulnerability Management](https://www.datadoghq.com/product/application-vulnerability-management/) - .log results file
* [Hdiv Detection (IAST)](https://hdivsecurity.com/interactive-application-security-testing-iast) - .hlg results file
* [Synopsys Seeker IAST](https://www.synopsys.com/software-integrity/security-testing/interactive-application-security-testing.html) - .csv results file

**Commercial Hybrid Analysis Application Security Testing Tools:**

* [Fusion Lite Insight](https://www.iappsecure.com/products.html) - .xml results file

**WARNING: If you generate results for a commercial tool, be careful who you distribute it to. Each tool has its own license defining when any results it produces can be released/made public. It may be against the terms of a commercial tool's license to publicly release that tool's score against the OWASP Benchmark. The OWASP Benchmark project takes no responsibility if someone else releases such results.**
