# Horizon Package Manager
Installing Horizon packages and dependencies made easy.

## Backend
### HPM Webserver
For API requests

Server - Kali Linux x64 (Debian) hosted as a VM on HyperV

Written in NodeJS 
### HPM Database
Stores packages, dependencies and install, update and uninstall commands for all of these

* **Table - Packages**
    * Columns - PackageGUID VARCHAR(36) PRIMARY KEY, PackageName VARCHAR(24), Version VARCHAR(10), VersionFile NTEXT
* **Table - Dependencies**
    * Columns - PackageGUID VARCHAR(36) FORIEGN KEY, DependencyGUID VARCHAR(36), Version VARCHAR(10), VersionFile NTEXT
* **Table - Installation**
    * Columns - PackageGUID VARCHAR(36) FORIEGN KEY, StepIndex INT, Step NTEXT
* **Table - Update**
    * Columns - PackageGUID VARCHAR(36) FORIEGN KEY, StepIndex INT, Step NTEXT
* **Table - Uninstall**
    * Columns - PackageGUID VARCHAR(36) FORIEGN KEY, StepIndex INT, Step NTEXT

## Commandline Tool
Install, update and uninstall Horizon Packages and dependencies

Written in Python and compiled into an exe on a 32bit Windows 7 build so it can be used on any Windows 7 or later with any CPU architecture 
### Logic 
#### Installing
1. Sends API request to webserver 
    1. Notifiy user if request was unsuccessful w/ failure reason
2. Package dependencies checked if they are already installed 
    1. If dependency is installed, check VersionFile if version matching or greater than version in db
       1. If less than version stored in db perform dependancy update command // check with user(advise suggesting it be completed)
    2. Dependency is installed if it is missing
3. Check if package is already installed 
    1. Check VersionFile if Version is latest
       1. Perform update if not // Check with user first
4. Store the version in VersionFile location
5. Package is then installed

#### Updating
1. Sends API request to webserver 
    1. Notifiy user if request was unsuccessful w/ failure reason
2. Package dependencies checked if they are already installed 
    1. If dependency is installed, check VersionFile if version matching or greater than version in db
       1. If less than version stored in db perform dependancy update command // check with user(advise suggesting it be completed)
    2. Dependency is installed if it is missing
3. Check if package is already installed 
    1. Check VersionFile if Version is latest
       1. Perform update if not
4. Update VersionFile to the new version
5. Package is then updated

#### Uninstalling
1. Send API request to webserver
    1. Notifiy user if request was unsuccessful w/ failure reason
2. Check if package is installed
    1. If package is installed perform uninstall steps
3. Send email to Support, Accounts, Joe, Jake, Sam and anyone else that wants to be added
