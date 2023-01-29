# API Test Automation using Postman

## Table of contents
- Introduction
- Requirements
- Installation
- Configuration
- Developers
- Maintainers


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
 
 
	![Alt text](C:\Users\Kristian\OneDrive\Dokumenti\slike_README.jpg)?raw=true "Postman"

### Help

### Authors

### Version History

### License

### Acknowledgements





