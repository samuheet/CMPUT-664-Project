# Comparision of Static Analysis tools to detect SQL Injection and Cross-site Scritping
A study of open-source and commercial static analysis tools to detect SQL Injection and Cross-site Scripting.
 
## Requirements

Open source tools:

1. [Visual Code Grepper](https://github.com/nccgroup/VCG)
2. [phpSAFE](https://github.com/JoseCarlosFonseca/phpSAFE)
3. [FPwFindSecBugs](https://github.com/find-sec-bugs/find-sec-bugs)
4. [SecureCodeScan](https://security-code-scan.github.io/)

Commercial tool:

This project uses the commercial version of [Coverity static analysis tool](https://community.synopsys.com/s/getting-started-with-synopsys#GSCoverity) and requires Coverity's Analysis license along with the Platform license. To run static analysis on Coverity, the code needs to be built with specific build tools or using IDE. For example, Java projects are commonly built using Maven or Ant. In this project, only Maven was required for Java. DotNET projects were built using Visual Studio 2019. PHP projects do not require to be built as they are considered to be just scripts/interpreted code. 

**Important:** 

Projects:

1. [OWASP Benchmark](https://github.com/OWASP/Benchmark) - A Java test suite designed to evaluate the accuracy, coverage, and speed of automated software vulnerability detection tools. 

2. [Vulnerable Web Application](https://github.com/OWASP/Vulnerable-Web-Application) - This PHP web app categorically includes Command Execution, File Inclusion, File Upload, SQL and XSS vulnerabilities.

3. [OWASP WebGoat.NET](https://github.com/OWASP/WebGoat.NET) - A vulnerable web application built on .NET Framework maintained by OWASP.


## Results
TO DO
