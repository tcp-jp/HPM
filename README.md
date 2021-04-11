# Horizon Package Manager
Installing Horizon packages and dependencies made easy.

## Backend
#### HPM Database
Table - Packages

Columns - PackageGUID VARCHAR(36) PRIMARY KEY, PackageName VARCHAR(24), Version VARCHAR(10), VersionFile NTEXT

Table - Dependencies

Columns - PackageGUID VARCHAR(36) FORIEGN KEY, DependencyGUID VARCHAR(36), Version VARCHAR(10), VersionFile NTEXT

Table - Installation

Columns - PackageGUID VARCHAR(36) FORIEGN KEY, StepIndex INT, Step NTEXT

Table - Update 

Columns - PackageGUID VARCHAR(36) FORIEGN KEY, StepIndex INT, Step NTEXT

Table - Uninstall

Columns - PackageGUID VARCHAR(36) FORIEGN KEY, StepIndex INT, Step NTEXT

## Commandline Tool

Install, update and uninstall Horizon Packages and dependencies

#### Logic 
##### Installing
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

##### Updating
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

4. Store the version in VersionFile location

##### Uninstalling

. Send email to Support, Accounts, Joe, Jake (anyone else that wants to be added)
