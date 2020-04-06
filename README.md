# Comparison of Static Analysis tools to detect SQL Injection and Cross-site Scritping
A study of open-source and commercial static analysis tools to detect SQL Injection and Cross-site Scripting.
 
## Requirements
To replicate this study, the below open-source tools and projects are required. Additionally, commercial Coverity licenses are needed. 

Open source tools:

1. [Visual Code Grepper](https://github.com/nccgroup/VCG)
2. [phpSAFE](https://github.com/JoseCarlosFonseca/phpSAFE)
3. [FPwFindSecBugs](https://github.com/find-sec-bugs/find-sec-bugs)
4. [SecureCodeScan](https://security-code-scan.github.io/)

Commercial tool:

This project uses the commercial version of [Coverity static analysis tool](https://community.synopsys.com/s/getting-started-with-synopsys#GSCoverity) and requires Coverity's Analysis license along with the Platform license. To run static analysis on Coverity, the code needs to be built with specific build tools or using IDE. For example, Java projects are commonly built using Maven or Ant. In this project, only Maven was required for Java. DotNET projects were built using Visual Studio 2019. PHP projects do not require to be built as they are considered to be just scripts/interpreted code. 

**Important:** Xampp is need to run phpSAFE.

Projects:

1. [OWASP Benchmark](https://github.com/OWASP/Benchmark) - A Java test suite designed to evaluate the accuracy, coverage, and speed of automated software vulnerability detection tools. 

2. [Vulnerable Web Application](https://github.com/OWASP/Vulnerable-Web-Application) - This PHP web app categorically includes Command Execution, File Inclusion, File Upload, SQL and XSS vulnerabilities.

3. [OWASP WebGoat.NET](https://github.com/OWASP/WebGoat.NET) - A vulnerable web application built on .NET Framework maintained by OWASP.


## Perform Static Analysis

**Coverity**


**Visual Code Grepper (VCG)**

To use VCG, download the repository from GitHub and go to the directory /VCG-Setup/Release/. 

1. Install the software using VCGSetup.msi file. 
2. Next, open the application which provides a GUI interface. 
3.Select the language of the project you want to scan, provide the path to project directory and run a full scan. Results are generated after the scan completes and can be exported to CSV/XML. Repeat this step with different projects. 

**phpSAFE**

To use phpSAFE, download the repository from GitHub. Install Xampp and start the Apache server. Go to installed directory where Xampp is installed. Navigate to \Xampp\htdocs and place the downloaded phpSAFE repository.  

1. In the copied phpSAFE repository available in \Xampp\htdocs, go to \Xampp\htdocs\test.
2. Place all the PHP files that need to be scanned into this directory.
3. Open a browser and type localhost\phpSAFE. 
4. Select the file that needs to be scanned and click on Analyze file.
5. Export the outputs.
6. Go back to the homepage and repeat the steps 4 to 6 for all the files.

Note: phpSAFE scans only one file at a time.

**Security Code Scan (SCS)**

SCS is available as an extension to the Visual Studio. It can also be added as a NuGet package to specific projects. 

1. Install SCS from the Visual Studio extension marketplace.
2. Open the Options dialog box, on the menu bar in Visual Studio choose Tools > Options. 
3. In the Options dialog box, choose Text Editor > C# or Basic > Advanced. Make sure that the "Full solution analysis" checkbox is checked. Otherwise, the scan occurs only for the current project.
4. Build the project in Visual Studio and go to the Error list tab to see the scan results.

**FPwFindSecBugs**

FPwFindSecBugs is available as a plugin to the Eclipse IDE. The analysis results of FPwFindSecBugs on the Benchmark project are available on the [OWASP Benchmark](https://owasp.org/www-project-benchmark/) website.


## Results
TODO
