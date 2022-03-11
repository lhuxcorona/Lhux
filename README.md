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

## Top-level directory
        
    ├── apps                   # Contains both android and IOS app files.
    ├── config                 # Contains all the configuration files where define desired capabilities for appium.
    ├── core                   # Base functions that any class can use.
    ├── node_modules           # Provides npm packages to the entire workspace.
    ├── src                    # Application source code.
    ├── tests                  # Contains all the tests for android and ios.
    ├── visual_regression      # Includes images used for test comparation.
    ├── .env                   # Environment variables that are used for local development.
    ├── .gitignore             # Specifies intentionally untracked files that Git should ignore.
    ├── package-lock.json      # Provides version information for all packages installed into node_modules by the npm client.
    ├── package.json           # Holds important information about the project.
    ├── tsconfig.json          # The base TypeScript configuration for projects in the workspaces.
    └── README.md              # Introductory documentation for the application. 
    

### config directory

 Within this directory  are the appium capabilities for the different platforms (Android & IO) as well as the configuration with headspin. 
 if some  specific capability  is needed, this is the place to put it
 
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

### core directory

Other files in the project inherit from this base files.

    .
    ├── ...
    ├── core                   
    │   ├── base.screen.ts     # Common or shared components 
    │   ├── element.ts         # Provides function for selection strategies to query an item
    │   ├── screen.factory.ts  # Provides the names of the different UI screens
    │   └── ...                 
    └── ...


### node_modules directory

Provides npm packages to the entire workspace. Workspace-wide node_modules dependencies are visible to all projects.

    .
    ├── ...
    ├── node_modules                   
    └── ...

### src directory

Application source code

    .
    ├── ...
    ├── src  #Source files for the root-level application project.                  
    │   ├── data    
    |            ├── loginData.js # Contains information for user authentication
    │   ├── helpers  # Helper functions and utility classes. Each helper file is simply a collection of functions in a particular category. 
    |            ├── android.permissions.ts #Provides several selection strategies to query an item related to mobile data permission such as location, camera, etc. on android
    |            ├── gestures.ts            # Holds functions of gestures are performed by the user's fingers (tap, swipe, drag, slide etc.) on the application.
    |            ├── ios.gallery.screen.ts  # Provides several selection strategies to query an item related to photopass gallery on IOS
    |            ├── ios.permissions.ts     # Provides several selection strategies to query an item related to mobile data permission such as location, camera, etc. on ios
    |            ├── util.ts                # Utility class stores and handles the functions (The code which is repetitive in nature) which can be commonly used across the entire framework.
    |            ├── validation.android.ts  # Contains methods that validate path for video and photo saved into the device
    |            ├── wait.actions.ts        # Contains functions that expects a condition and waits until that condition is fulfilled with a truthy value for differents elements
    │   ├── screens  # Contains files that  belongs to one UI page in the application and are common to android and ios. This page class will identify the UI Elements of that page and also contains methods which perform operations on those UI Elements. For each UI page in the application, there is a corresponding Page Class
    |            ├── android                # Contains files that  belongs to one UI page in the application on platform Android             
    |            ├── ios                    # Contains files that  belongs to one UI page in the application on platform IOS
    │   ├── steps  # Includes Gherkin step files for  differents scenarios in the application 
    |            ├── given.ts               # Describe an initial context  (Given steps) base on Gherkin languaje
    |            ├── hooks.ts               # Run functions before or after the test. It includes features like login and some pre-steps for app login.
    |            ├── when.ts.ts             # Describe an event (When steps) base on Gherkin languaje
    |            ├── then.ts.ts             # Describe an expected outcome (Then steps) base on Gherkin languaje
    │   ├── types  # Additional capabilities   
    |            ├── types.d.ts             # Additional libraries from typescript
    |            ├── wdio.d.ts              # functions that helps in order to compare images
    │   ├── test  #  add use cases in this directory
    |            ├── android                # All the tests for android are kept in this folder, it holds test case development based on functional requirements.
    |            ├── ios                    # All the tests for ios are kept in this folder, it holds test case development based on functional requirements.
    │   └── ...                 
    └── ...


### visual_regression directory

Includes images used for test comparation.

    .
    ├── ...
    ├── visual_regression                   
    └── ...


