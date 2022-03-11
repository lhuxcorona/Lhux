# AR+/LaL :

## Table of Contents
1. [General Info](#general-info)
2. [Technologies](#technologies)
3. [Installation](#installation)
4. [Project setup](#project-setup)
5. [Project structure](#project-structure)


# General Info

Mobile automation project for AR+/LaL Android and iOS apps with  Appium,  Webdriver IO using the  best practices with page objects (POM)
This includes testing UI using creation of automated functional test cases and running them against application under test on one or more devices.
The test results are  transformed into html format for reporting purpose using Allure Report
This  tool will help us in reducing the testing time cycle.

link de casos de uso --- Emanuel

# Technologies

* WebdriverIO 7.16.16
* TypeScript 4.3.2
* Appium
* Allure Report 


# Installation

## Requirements

- Disney Network account
- Access to disney's VPN
- Disney Certificate [Certificate](https://enroll.disney.pvt/rootcerts.stm)

## Software Requirements

* Node  14.17.0   [Node](https://nodejs.org/es/download/)
* Homebrew  latest version [Homebrew](https://docs.brew.sh/Installation)
* Git latest version [Git](https://git-scm.com/downloads)
* Java latest version [Java](https://www.oracle.com/java/technologies/downloads/)
* XCode latest version (download from app store)
* Command Line Tools for XCode latest version (download from app store)
* Android Studio and the Android SDK [Android](https://developer.android.com/)
* Cucumber (install Cucumber (Gherkin) Full Support extension in VSC  )
    
## Hardware Requirements
* Mobile device OS Platform Android
* Mobile device OS Platform IOS
    
## Software Installation / Configuration

###  Install Node Version Manager nvm  and Node on macOS

Assuming that Homebrew is already installed, type:
```
brew update
brew install nvm 
```
Next, create a directory for NVM in home.
```
mkdir ~/.nvm
```
Add below lines to ~/.bash_profile ( or ~/.zshrc for macOS Catalina or later)
```
export NVM_DIR=~/.nvm
source $(brew --prefix nvm)/nvm.sh
```

Reload the shell configuration by using the following command
```
source ~/.zshrc
```

Install the specific version
```
nvm install v14.17.0
```

Next, you actually have to use that specific version of Node that you just installed
```
nvm use v14.17.0
```

Verify the installation
```
node —version
npm version
```
# Project setup


- Clone the  project `ar-plus/mobile_automation` using the URL `git@github.disney.com:ar-plus/mobile_automation.git` to your local machine

- In VSCode select  `File > Open Folder `  and browse to your project folder that you cloned from previous step

- In order to speed up the development process, install  `Cucumber (Gherkin) Full Support, Beautify, TypeScript Nightly and DotENV ` extensions in VSCode


### How to run the project on a physical device on android

Connect your device over USB

Verify that your operating system is able to see your device, type  `adb devices ` on a terminal, it should appear the list of devices attached

Copy the name and characteristics of the device in the configuration file  wdio.android.conf for Android in the capabilities of appium

Open a terminal from VSC and run the test script you are  interest in, for instance:
`/node_modules/.bin/wdio ./config/wdio.android.conf.ts --spec ./tests/android/ar.permissions.feature`

### How to run the project on a physical device ios
TODO

### How to run with headspin

You must be connected to the disney vpn

Open a terminal from VSCode and run the test script you are  interest in for instance:

`npm run headspin.android.stage -- --spec "tests/android/ar.comparation.images.feature `

# Project structure

## top-level directory
        
    ├── apps                   # Contains both android and IOS app files
    ├── config                 # Contains all the configuration files where define desired capabilities for appium
    ├── core                   # Base functions that any class can use
    ├── src                    # Source files for the root-level application project.
    ├── tests                  # Contains all the tests for android and ios
    ├── visual_regression      # Includes images used for test comparation 
    ├── .env                   # Environment variables that are used for local development
    ├── .gitignore             # Specifies intentionally untracked files that Git should ignore.
    ├── package-lock.json      # Provides version information for all packages installed into node_modules by the npm client
    ├── package.json           # Holds important information about the project.
    ├── tsconfig.json          # The base TypeScript configuration for projects in the workspaces
    └── README.md              # Introductory documentation for the application. 
    

### config directory

 Within this directory  are the appium capabilities for the different platforms (Android & IO) as well as the configuration with headspin. 
 If you need to add any specific capabilities this is the place to put it.
 
     .
     ├── ...
     ├── config                   
     │   ├── wdio.android.conf.ts                    # Config capabilities for Android
     │   ├── wdio.android.weak.connection.config.ts  # Config specific capabilities for weak connection
     │   ├── wdio.headspin.android.conf.ts           # Config capabilities for Headspin-Android
     │   ├── wdio.headspin.ios.conf.ts               # Config capabilities for Headspin-IOS
     │   ├── wdio.headspin.shared.config.ts          # Config shared capabilities for headspin
     │   ├── wdio.ios.real.device.ts                 # Config specific capabilities
     │   ├── wdio.shared.conf.ts                     # Config shared capabilities for both android and ios
     │   └── ...                 
     └── ...

##### core lux

Other files in the project inherit from this base files.

##### node_modules

Provides npm packages to the entire workspace. Workspace-wide node_modules dependencies are visible to all projects.

##### src

Source files for the root-level application project.

##### src > data > loginData.js

Contains  information for user authentication

##### src > data > helpers

Helpers, as the name suggests, help with some common tasks. Each helper file is simply a collection of functions in a particular category.

##### src > data > helpers > android.permissions.ts

Provides several selection strategies to query an item related to mobile data permission such as location, camera, etc. on android

##### src > data > helpers > app.info.screen.ts Remover parece estar duplicado
Provides several selection strategies to query an item related to mobile data permission such as location, camera, etc. TODO

##### src > data > helpers > gestures.ts

Holds functions of gestures are performed by the user's fingers (tap, swipe, drag, slide etc.) on the application.

##### src > data > helpers > ios.gallery.screen.ts

Provides several selection strategies to query an item related to photopass gallery on IOS

##### src > data > helpers > ios.permissions.ts

Provides several selection strategies to query an item related to mobile data permission such as location, camera, etc. on ios

##### src > data > helpers > utils.ts

Utility class stores and handles the functions (The code which is repetitive in nature) which can be commonly used across the entire framework.

##### src > data > helpers > validation.android.ts

Contains methods that validate path for video and photo saved into the device

##### src > data > helpers > wait.actions.ts

Contains functions that expects a condition and waits until that condition is fulfilled with a truthy value for differents elements

##### src > screens

Contains files that  belongs to one UI page in the application and are common to android and ios. This page class will identify the UI Elements of that page and also contains methods which perform operations on those UI Elements.

##### src > screens > android

Contains files that  belongs to one UI page in the application on platform Android

##### src > screens > ios

Contains files that  belongs to one UI page in the application on platform IOS

##### src > steps

Includes Gherkin step files for  differents scenarios in the application

##### src > steps > given.ts

Describe an initial context  (Given steps) base on Gherkin languaje

##### src > steps > hooks.ts 

Run functions before or after the test. It includes features like login and some pre-steps for app login.

##### src > steps > when.ts

Describe an event (When steps) base on Gherkin languaje

##### src > steps > then.ts

Describe an expected outcome (Then steps) base on Gherkin languaje

##### src > types >
TODO
agregar libreria de typescri
nuevas funcionalidades 



##### src > tests > android

All the tests for android are kept in this folder, it holds test case development based on functional requirements.

##### src > tests > ios

All the tests for ios are kept in this folder, it holds test case development based on functional requirements.

##### visual_regression
TODO


##### .env

Contains variables that are used to run the test on headspin

##### .gitignore

Specifies intentionally untracked files that Git should ignore.

##### package-lock.json

Provides version information for all packages installed into node_modules by the npm client

##### package.json

Holds important information about the project. It contains  metadata about the project (like the project name and description) as well as functional metadata like the package version number and a list of dependencies required by the application.

##### README.md

Introductory documentation for the application. 

##### tsconfig.json

The base TypeScript configuration for projects in the workspace

