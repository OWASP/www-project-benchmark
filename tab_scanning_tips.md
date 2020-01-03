---
title: Scanning_Tips
displaytext: Tool Scanning Tips
layout:  null
tab: true
order: 5
tags: benchmark
---

People frequently have difficulty scanning the Benchmark with various tools due to many reasons, including size of the Benchmark app and its codebase, and complexity of the tools used. Here is some guidance for some of the tools we have used to scan the Benchmark. If you've learned any tricks on how to get better or easier results for a particular tool against the Benchmark, let us know or update this page directly.

## Generic Tips ##
Because of the size of the Benchmark, you may need to give your tool more memory before it starts the scan. If its a Java based tool, you may want to pass more memory to it like this:
    Shell
    -Xmx4G (This gives the Java application 4 Gig of memory)


## SAST Tools ##
**Checkmarx**

The Checkmarx SAST Tool (CxSAST) is ready to scan the OWASP Benchmark out-of-the-box. Please notice that the OWASP Benchmark �hides� some vulnerabilities in dead code areas, for example:
    code()
    if (0>1)
    {
      //vulnerable code
    }

By default, CxSAST will find these vulnerabilities since Checkmarx believes that including dead code in the scan results is a SAST best practice.

Checkmarx's experience shows that security experts expect to find these types of code vulnerabilities, and demand that their developers fix them. However, OWASP Benchmark considers the flagging of these vulnerabilities as False Positives, as a result lowering Checkmarx's overall score.

Therefore, in order to receive an OWASP score untainted by dead code, re-configure CxSAST as follows:

1. Open the CxAudit client for editing Java queries.
2. Override the "Find_Dead_Code" query.
3. Add the commented text of the original query to the new override query.
4. Save the queries.

**Kiuwan Code Security**

Kiuwan Code Security wrote their own instructions for scanning the OWASP Benchmark. Refer to their [step-by-step guide](https://www.kiuwan.com/blog/owasp-benchmark-diy/) on the Kiuwan website.

**Micro Focus (Formally HP) Fortify**

If you are using the Audit Workbench, you can give it more memory and make sure you invoke it in 64-bit mode by doing this:
    Shell
    set AWB_VM_OPTS="-Xmx2G -XX:MaxPermSize=256m"
    export AWB_VM_OPTS="-Xmx2G -XX:MaxPermSize=256m"
    auditworkbench -64

We found it was easier to use the Maven support in Fortify to scan the Benchmark and to do it in 2 phases, translate, and then scan. We did something like this:
    Shell
    Translate Phase:
    export JAVA_HOME=$(/usr/libexec/java_home)
    export PATH=$PATH:/Applications/HP_Fortify/HP_Fortify_SCA_and_Apps_17.10/bin
    export SCA_VM_OPTS="-Xmx2G -version 1.7"
    mvn sca:clean
    mvn sca:translate


    Shell
    Scan Phase:
    export JAVA_HOME=$(/usr/libexec/java_home)
    export PATH=$PATH:/Applications/HP_Fortify/HP_Fortify_SCA_and_Apps_4.10/bin
    export SCA_VM_OPTS="-Xmx10G -version 1.7"
    mvn sca:scan


**PMD**

We include this free tool in the Benchmark and its all dialed in. Simply run the script: ./script/runPMD.(sh or bat). If you want to run a different version of PMD, just change its version number in the Benchmark pom.xml file. (NOTE: PMD doesn't find any security issues. We include it because its interesting to know that it doesn't.)

**SpotBugs**

We include this free tool in the Benchmark and its all dialed in. Simply run the script: ./script/runSpotBugs.(sh or bat). If you want to run a different version of SpotBugs, just change its version number in the Benchmark pom.xml file.

**SpotBugs with FindSecBugs**

[FindSecurityBugs](http://h3xstream.github.io/find-sec-bugs/) is a great plugin for SpotBugs that significantly increases the ability for SpotBugs to find security issues. We include this free tool in the Benchmark and its all dialed in. Simply run the script: ./script/runFindSecBugs.(sh or bat). If you want to run a different version of FindSecBugs, just change the version number of the findsecbugs-plugin artifact in the Benchmark pom.xml file.

**Xanitizer**

The vendor has written their own guide to [How to Set Up Xanitizer for OWASP Benchmark](http://www.rigs-it.net/opendownloads/whitepapers/HowToSetUpXanitizerForOWASPBenchmarkProject.pdf).

## DAST Tools ##
**Burp Pro**

To scan, first spider the entire Benchmark, and then select the /Benchmark URL and actively scan that branch. You can skip all the .html pages and any other pages that Burp says have no parameters.

NOTE: We have been unable to simply run Burp Pro against the entire Benchmark in one shot. In our experience, it eventually freezes/stops scanning. We've had to run it against each vulnerability area one at a time. If you figure out how to get Burp Pro to scan all of Benchmark in one shot, let us know how you did it!

**OWASP ZAP**

ZAP may require additional memory to be able to scan the Benchmark. To configure the amount of memory:
* Tools --> Options --> JVM: Recommend setting to: -Xmx2048m (or larger). (Then restart ZAP).

To run ZAP against Benchmark:
1. Because Benchmark uses Cookies and Headers as sources of attack for many test cases: Tools --> Options --> Active Scan Input Vectors: Then check the HTTP Headers, All Requests, and Cookie Data checkboxes and hit OK
2. Click on Show All Tabs button (if spider tab isn't visible)
3. Go to Spider tab (the black spider) and click on New Scan button
4. Enter: https://localhost:8443/benchmark/ into the 'Starting Point' box and hit 'Start Scan'
	* Do this again. For some reason it takes 2 passes with the Spider before it stops finding more Benchmark endpoints.
5. When Spider completes, click on 'benchmark' folder in Site Map, right click and select: 'Attack --> Active Scan'
	* It will take several hours, like 3+ to complete (it's actually likely to simply freeze before completing the scan - see NOTE: below)

For faster active scan you can:
* Disable the ZAP DB log (in ZAP 2.5.0+):
	* Disable it via Options / Database / Recover Log
	* Set it on the command line using "-config database.recoverylog=false"
* Disable unnecessary plugins / Technologies: When you launch the Active Scan
	* On the Policy tab, disable all plugins except: XSS (Reflected), Path Traversal, SQLi, OS Command Injection
	* Go the Technology Tab, disable everything and only enable: MySQL, YOUR_OS, Tomcat
	* Note: This 2nd performance improvement step is a bit like cheating as you wouldn't do this for a normal site scan. You'd want to leave all this on in case these other plugins/technologies are helpful in finding more issues. So a fair performance comparison of ZAP to other tools would leave all this on.

To generate the ZAP XML results file so you can generate its scorecard:
* Tools > Options > Alerts - And set the Max alert instances to like 500.
* Then: Report > Generate XML Report...
NOTE: Similar to Burp, we can't simply run ZAP against the entire Benchmark in one shot. In our experience, it eventually freezes/stops scanning. We've had to run it against each test area one at a time. If you figure out how to get ZAP to scan all of Benchmark in one shot, let us know how you did it!

Things we tried that didn't improve the score:
* AJAX Spider - the traditional spider appears to find all (or 99%) of the test cases so the AJAX Spider does not appear to be needed against Benchmark v1.2
* XSS (Persistent) - There are 3 of these plugins that run by default. There aren't any stored XSS in Benchmark, so you can disable these plugins for a faster scan.
* DOM XSS Plugin - This is an optional plugin that didn't seem to find any additional XSS issues. There aren't an DOM specific XSS issues in Benchmark v1.2, so not surprising.

## IAST Tools ##
Interactive Application Security Testing (IAST) tools work differently than scanners. IAST tools monitor an application as it runs to identify application vulnerabilities using context from inside the running application. Typically these tools run continuously, immediately notifying users of vulnerabilities, but you can also get a full report of an entire application. To do this, we simply run the Benchmark application with an IAST agent and use a crawler to hit all the pages.

**Contrast Assess**

To use Contrast Assess, we simply add the Java agent to the Benchmark environment and run the BenchmarkCrawler. The entire process should only take a few minutes. We provided a few scripts, which simply add the -javaagent:contrast.jar flag to the Benchmark launch configuration. We have tested on MacOS, Ubuntu, and Windows. Be sure your VM has at least 4M of memory.

* Ensure your environment has Java, Maven, and git installed, then build the Benchmark project
    Shell
      $ git clone https://github.com/OWASP/Benchmark.git
      $ cd Benchmark
      $ mvn compile

* Download a licensed copy of the Contrast Assess Java Agent (contrast.jar) from your Contrast TeamServer account and put it in the /Benchmark/tools/Contrast directory.
    Shell
      $ cp ~/Downloads/contrast.jar tools/Contrast

* In Terminal 1, launch the Benchmark application and wait until it starts
    Shell
      $ cd tools/Contrast  
      $ ./runBenchmark_wContrast.sh (.bat on Windows)
      [INFO] Scanning for projects...
      [INFO]                                                                         
      [INFO] ------------------------------------------------------------------------
      [INFO] Building OWASP Benchmark Project 1.2
      [INFO] ------------------------------------------------------------------------
      [INFO] 
      ...
      [INFO]_[talledLocalContainer] Tomcat 8.x started on port [8443]
      [INFO] Press Ctrl-C to stop the container...

* In Terminal 2, launch the crawler and wait a minute or two for the crawl to complete.
    Shell
      $ ./runCrawler.sh (.bat on Windows)

* A Contrast report has been generated in /Benchmark/tools/Contrast/working/contrast.log. This report will be automatically copied (and renamed with version number) to /Benchmark/results directory.
    Shell
      $ more tools/Contrast/working/contrast.log
      2016-04-22 12:29:29,716 [main b] INFO - Contrast Runtime Engine
      2016-04-22 12:29:29,717 [main b] INFO - Copyright (C) 2019
      2016-04-22 12:29:29,717 [main b] INFO - Pat. 8,458,789 B2
      2016-04-22 12:29:29,717 [main b] INFO - Contrast Security, Inc.
      2016-04-22 12:29:29,717 [main b] INFO - All Rights Reserved
      2016-04-22 12:29:29,717 [main b] INFO - https://www.contrastsecurity.com/
      ...

* Press Ctrl-C to stop the Benchmark in Terminal 1. Note: on Windows, select "N" when asked Terminate batch job (Y/N))
    Shell
      [INFO]_[talledLocalContainer] Tomcat 8.x is stopped
      Copying Contrast report to results directory

* In Terminal 2, generate scorecards in /Benchmark/scorecard
    Shell
      $ ./createScorecards.sh (.bat on Windows)
      Analyzing results from Benchmark_1.2-Contrast.log
      Actual results file generated: /Users/owasp/Projects/Benchmark/scorecard/Benchmark_v1.2_Scorecard_for_Contrast.csv
      Report written to: /Users/owasp/Projects/Benchmark/scorecard/Benchmark_v1.2_Scorecard_for_Contrast.html

* Open the Benchmark Scorecard in your browser
    Shell
      /Users/owasp/Projects/Benchmark/scorecard/Benchmark_v1.2_Scorecard_for_Contrast.html
      

**Hdiv Detection**

Hdiv has written their own instructions on how to run the detection component of their product on the Benchmark here: https://hdivsecurity.com/docs/features/benchmark/#how-to-run-hdiv-in-owasp-benchmark-project. You'll see that these instructions involve using the same crawler used to exercise all the test cases in the Benchmark, just like Contrast above.
