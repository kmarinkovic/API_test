# API Test Automation using Postman

## Table of contents
- Introduction
- Requirements
- Installation
- Configuration


### Introduction

Aim of this project is to create an automated test suite for a sample RESTful API.
API can be found on [https://crudcrud.com] which supports standard CRUD (Create, Read, Update and Delete) operations.
This project uses Postman as an API testing and automation tool.

Some of the Postman advantages include:
* Suited for exploratory, manual and automation testing
* Easy to create, share, test and document APIs
* Simple to build and send requests and examine responses
* Store information for running tests in different environments
* Easy to move tests and environments to code repositories


### Requirements
- installed Postman API tool
- installed Newman CLI (with Node.js and NPM - Node package manager)
- installed Jenkins CI/CD


### Installation
1. **Postman**
	* go to [https://www.postman.com/downloads/] and download the app (Windows, Mac, Linux) to get started

2. **Newman CLI**

	* before installing Newman, we need to install Node.js and NPM

  *Windows*:
* Open your Command prompt
* Type the following: node -v
* If you see a version number, then you have node.js previously installed and do not need anything else to do, else navigate to [https://nodejs.org/en/download] and click on "Windows Installer" -> npm is part of installation
* update "npm" that comes with installer: npm install npm --global
* install newman : "npm install -g newman"
* check if newman is successfully installed : newman -v
	


  *Linux*:
* Open your Terminal
* Type the following :sudo apt install nodejs; curl -L https://npmjs.org/install.sh | sudo sh
* Set NODE HOME in enviroment variable: export PATH=/usr/local/git/bin:/usr/local/bin:$PATH
* install newman : "npm install -g newman"
* check if newman is successfully installed : newman -version

  *MacOS*
* Open your Terminal
* Navigate to [https://nodejs.org/en/download] and click on    "macOS Installer" and save it
* Run installer
* Verify successful installation of Node.js with "node -v"
* Update your npm version: "sudo npm install npm --global"
* Set NODE HOME in enviroment variable: export PATH=/usr/local/git/bin:/usr/local/bin:$PATH 
* install newman : "npm install -g newman"
* check if newman is successfully installed : newman -version



3. **Jenkins**
* Go to [https://www.jenkins.io/downloads] and download the app (Windows, Mac, Linux) to get started
* Before installing make sure you have Java (11 or 17) installed 
* After completing the Jenkins installation process, a browser tab will pop-up asking for the initial Administrator password. To access Jenkins, you need to go [http://localhost:8080] in your web browser.The initial administrator password should be found under the Jenkins installation path (\Jenkins\secrets)





### Configuration

#### Getting started
Before you can start running tests, first you need to import Postman collection (Postman Collections/postman_tests.json)
* My Workspace -> Import -> Choose Files


After import, you should be able to see collection "API_test" with prepared requests.

#### Executing testcases

Postman has a powerful runtime based on Node.js that allows for addition of dynamic behaviour to requests and collections. This allows to write API tests, build requests that can contain dynamic parameters, pass data between requests etc. Examples of small JavaScript code (snippets) are available in Postman for reference.


#### 1.Run requests
To run requests, you highlight request and click on "Send" button. If available, response body is displayed in lower window. In upper window you can toggle between different tabs (Params, Authorization, Headers,...). Testcases for each request are written under "Tests" tab and are run after request is sent to check for expected values.

#### 2.Run collection from Postman
To run complete collection from Postman, select "API_test" and from the dropdown menu on the right choose "Run collection". "Run manually" option will run all requests with tests inside Postman.

#### 3.Run collection using Newman
To run collection using Newman, start Command prompt (Terminal for Mac and Linux) and execute:

newman run "collection_url"/?access_key=ACCESS_KEY --env-var url=https://crudcrud.com/api/79867d1527f14b81ada642d3402104a2/items --env-var id

where "collection url" and ACCESS_KEY can be obtained from "Share" option (Via API) on "API_test" collection in Postman

#### 4.Run collection using Jenkins job
First we need to create a new Jenkins job:
New Item -> name e.g Postman Collection and choose Freestyle project.
In project Postman Collection choose Configure -> Build and click on "Execute Windows Batch Command" (if using Windows) or "Execute shell" (when using Mac or Linux).  

Additionally commands to generate reports were added.  
To set publishing HTML reports, choose Configure -> Post-build Actions -> Publish HTML reports:
- HTML directory to archive : newman
- Index page: myHTMLreport.html  
- Report title: HTML report  

To set publishing Junit reports, choose Configure -> Post-build Actions -> Publish JUnit test result report:
- Test report XMLs : newman/myreport.xml 


Add newman run command: 
C:\"path_to_newman_script"\newman run "collection_url"/?access_key=ACCESS_KEY --env-var url=https://crudcrud.com/api/79867d1527f14b81ada642d3402104a2/items --env-var id --disable-unicode --reporters cli,html,junit --reporter-junit-export "newman/myreport.xml" --reporter-html-export "newman/myHTMLreport.html"


XML and HTML results generated by Jenkins are available under Workspace-> newman -> myreport.xml and myHTMLreport.html

Testcase documentation is available under Testcases\Testcases_documentation.md








