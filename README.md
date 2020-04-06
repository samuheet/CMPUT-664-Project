# Comparison of Static Analysis tools to detect SQL Injection and Cross-site Scritping
A study of open-source and commercial static analysis tools to detect SQL Injection and Cross-site Scripting.
 
## Requirements
To replicate this study, the below open-source tools and projects are required. Additionally, commercial Coverity licenses are needed. All the softwares below are run on Windows but the instructions are also valid for other operating systems. 

Open source tools:

1. [Visual Code Grepper](https://github.com/nccgroup/VCG)
2. [phpSAFE](https://github.com/JoseCarlosFonseca/phpSAFE)
3. [SecureCodeScan](https://security-code-scan.github.io/)
4. [FPwFindSecBugs](https://github.com/find-sec-bugs/find-sec-bugs)

Commercial tool:

This project uses the commercial version of [Coverity static analysis tool](https://community.synopsys.com/s/getting-started-with-synopsys#GSCoverity) and requires Coverity's Analysis license along with the Platform license. To run static analysis on Coverity, the code needs to be built with specific build tools or using IDE. For example, Java projects are commonly built using Maven or Ant. In this project, only Maven was required for Java. DotNET projects were built using Visual Studio 2019. PHP projects do not require to be built as they are considered to be just scripts/interpreted code. 

**Important:** Xampp is need to run phpSAFE.

Open-source web projects:

1. [OWASP Benchmark](https://github.com/OWASP/Benchmark) - A Java test suite designed to evaluate the accuracy, coverage, and speed of automated software vulnerability detection tools. 

2. [Vulnerable Web Application](https://github.com/OWASP/Vulnerable-Web-Application) - This PHP web app categorically includes Command Execution, File Inclusion, File Upload, SQL and XSS vulnerabilities.

3. [OWASP WebGoat.NET](https://github.com/OWASP/WebGoat.NET) - A vulnerable web application built on .NET Framework maintained by OWASP.


## Perform Static Analysis

**Coverity**

Install Coverity Connect Server and configure a new server on your local machine. Install the Coverity Platform Analysis software. The Coverity Platform Analysis is basically a wizard which enables users to scan the source code.

Open the Coverity wizard and go to File -> click on "new configuration". Enter a name for your configuration. Click next. In the Working Directory, provide path to the project that needs to be scanned. In Intermediate directory section, provide the path where you want the ouput to be generated. 

Next, follow the instructions depending on your project.

* Settings for Java projects:

All Java projects can be build using the command line.
1. Select the Compiled Code checkbox and uncheck the Scripts or Interpreted Code checkbox.
2. Select the Command line build radio button.
3. Enter the 'Clean' and 'Build' commands depending upon the build tool ([Maven](https://maven.apache.org/install.html) or [Ant](https://ant.apache.org/manual/install.html) build) used in the project. For Maven, use 'mvn clean' and 'mvn install'. For Ant, use 'ant clean' and 'ant' commands.
4. Click on Capture Build.

* Settings for C# projects:

Command line build for C# was not used in this project instead C# projects were build using the Visual Studio IDE (not to be confused with VS Code). It is simpler for C# projects to build using an IDE. 
1. Select the Compiled Code checkbox and uncheck the Scripts or Interpreted Code checkbox.
2. Select the IDE build radio button.
3. Provide the path to the executable file of IDE i.e. path to Visual Studio.exe.
4. Click on Capture Build. This will open Visual Studio (VS). In VS, open the project that you intended to scan. Then, build the entire Solution. 
5. After the Solution is built, close Visual Studio and Coverity wizard automatically recognizes the build. 

* Settings for PHP projects:

PHP files are regarded as Scripts or Interpreted Code so, they need not be built.
1. Select the Scripts or Interpreted Code checkbox and uncheck the Compiled Code checkbox.
2. Click on Capture Build. If you see an error like 'No files found to scan', click on the Edit Buildless Capture Settings button. Delete the current path available in the list and manually add the path to the project. 

Once the build is captured, move to the next tab i.e. Analysis tab in the Coverity wizard. Click on Run Analysis. This step will take some time, depending on the size of your project. This is the step where Coverity performs the analysis. 

After the analysis is completed, click next to go to the Commits tab. In this tab, provide the address of your local Coverity server that you configured while installing the Coverity Server (example:http://laptop-2v2xxx88:8080/). Click on Commit Defects and the scanned defects are commited to your local server where you can view, track and export the bugs using the same above server URL (http://laptop-2v2xxx88:8080/).
         
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
