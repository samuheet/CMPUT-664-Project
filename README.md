# Comparison of Static Analysis tools to detect SQL Injection and Cross-site Scripting
A study of open-source and commercial static analysis tools to detect SQL Injection and Cross-site Scripting.
 
## Requirements
To replicate this study, the below open-source tools and projects are required. Additionally, commercial Coverity licenses are needed. All the tools below are used on Windows but the instructions are also valid for other operating systems. 

Open source tools:

1. [Visual Code Grepper](https://github.com/nccgroup/VCG)
2. [RIPS](http://rips-scanner.sourceforge.net/)
3. [SecureCodeScan](https://security-code-scan.github.io/)
4. [OWASP-ZAP](https://owasp.org/www-project-zap/)

Commercial tool:

This project uses the commercial version of [Coverity static analysis tool](https://community.synopsys.com/s/getting-started-with-synopsys#GSCoverity) and requires Coverity's Analysis license along with the Platform license. To run static analysis on Coverity, the code needs to be built with specific build tools or using IDE. For example, Java projects are commonly built using Maven or Ant. In this project, only Maven was required for Java. DotNET projects were built using Visual Studio 2019. PHP projects do not require to be built as they are considered scripts/interpreted code. 

Open-source web projects:

1. [OWASP Benchmark](https://github.com/OWASP/Benchmark) - A Java test suite designed to evaluate the accuracy, coverage, and speed of automated software vulnerability detection tools. 

2. [PHP Vulnerability Test Suite](https://samate.nist.gov/SARD/testsuite.php) - This PHP test suite is developed by the National Institute of Standards and Technology (NIST) categorically includes Command Execution, File Inclusion, File Upload, SQL and XSS vulnerabilities.

3. [OWASP WebGoat.NET](https://github.com/OWASP/WebGoat.NET) - A vulnerable web application built on .NET Framework maintained by OWASP.


## Perform Static Analysis

**Coverity**

Install Coverity Connect Server and configure a new server on your local machine. Install the Coverity Platform Analysis software. The Coverity Platform Analysis is a wizard that enables users to scan the source code.

Open the Coverity wizard and go to File -> click on "new configuration". Enter a name for your configuration. Click next. In the Working Directory, provide path to the project that needs to be scanned. In the Intermediate directory section, provide the path where you want the output to be generated. 

Next, follow the instructions depending on your project.

* Settings for Java projects: All Java projects can be build using the command line.
1. Select the Compiled Code checkbox and uncheck the Scripts or Interpreted Code checkbox.
2. Select the Command line build radio button.
3. Enter the 'Clean' and 'Build' commands depending upon the build tool ([Maven](https://maven.apache.org/install.html) or [Ant](https://ant.apache.org/manual/install.html) build) used in the project. For Maven, use 'mvn clean' and 'mvn install'. For Ant, use 'ant clean' and 'ant' commands.
4. Click on Capture Build.

* Settings for C# projects: Command line build for C# was not used in this project instead C# projects were build using the Visual Studio IDE (not to be confused with VS Code). To explore how Coverity can build using IDE, the IDE Build option was chosen. However, the command line build can be done by 'dotnet clean' and 'dotnet build'.   
1. Select the Compiled Code checkbox and uncheck the Scripts or Interpreted Code checkbox.
2. Select the IDE build radio button.
3. Provide the path to the executable file of IDE i.e. path to Visual Studio.exe.
4. Click on Capture Build. This will open Visual Studio (VS). In VS, open the project that you intended to scan. Then, build the entire Solution. 
5. After the Solution is built, close Visual Studio and Coverity wizard automatically recognizes the build. 

* Settings for PHP projects: PHP files are regarded as Scripts or Interpreted Code so, they need not be built.
1. Select the Scripts or Interpreted Code checkbox and uncheck the Compiled Code checkbox.
2. Click on Capture Build. If you see an error like 'No files found to scan', click on the Edit Buildless Capture Settings button. Delete the current path available on the list and manually add the path to the project. 

Once the build is captured, move to the next tab i.e. Analysis tab in the Coverity wizard. Click on Run Analysis. This step will take some time, depending on the size of your project. This is the step where Coverity performs the analysis. 

After the analysis is completed, click next to go to the Commits tab. In this tab, provide the address of your local Coverity server that you configured while installing the Coverity Server (example:http://laptop-2v2xxxxx:8080/). Click on Commit Defects and the scanned defects are committed to your local server where you can view, track and export the bugs using the same above server URL (http://laptop-2v2xxxxx:8080/).
         
**Visual Code Grepper (VCG)**

To use VCG, download the repository from GitHub and go to the directory /VCG-Setup/Release/. 

1. Install the software using VCGSetup.msi file. 
2. Next, open the application which provides a GUI interface. 
3. Select the language of the project you want to scan, provide the path to project directory and run a full scan. Results are generated after the scan completes and can be exported to CSV/XML. Repeat this step with different projects. 

**RIPS**

To use RIPS, download the repository from SourceForge. Install Xampp and start the Apache server. Go to the installed directory where Xampp is installed. Navigate to \Xampp\htdocs and place the downloaded RIPS repository.  

1. Open a browser and type localhost\RIPS. 
2. Select the directory that needs to be scanned and start the scan.
3. Export the outputs.

**Security Code Scan (SCS)**

SCS is available as an extension to the Visual Studio. It can also be added as a NuGet package to specific projects. 

1. Install SCS from the Visual Studio extension marketplace.
2. Open the Options dialog box, on the menu bar in Visual Studio choose Tools > Options. 
3. In the Options dialog box, choose Text Editor > C# or Basic > Advanced. Make sure that the "Full solution analysis" checkbox is checked. Otherwise, the scan occurs only for the current project.
4. Build the project in Visual Studio and go to the Error list tab to see the scan results.

**OWASP-ZAP**

Zed Attack Proxy (ZAP) is a free, open-source penetration testing tool being maintained by Open Web Application Security Project (OWASP). ZAP is designed specifically for testing web applications and is both flexible and extensible. It supports Java 1.8 and above. The results of ZAP are available in the OWASP Benchmark repository.


## Results

Coverity finds all the true positives for OWASP Benchmark project and misses two true positives in the WebGoat.NET project. Coverity does not perform very well on the PHP Vulnerable Test Suite.
