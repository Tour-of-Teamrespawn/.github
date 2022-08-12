# Adding a mission to the Tour organisation

Request access to the Organization from a server admin for if you have not done already (<https://github.com/Tour-of-Teamrespawn>)



## One-time config

These steps assume you are starting from scratch, and these sections only need to be done the once. Unless you buy a new PC or create a new user account of course...

### Prerequisites

Install git for Windows (<https://git-scm.com/download/win>). During the installer, make sure to change the git editor from VIM to "Visual Studio Code" to make further editing easier.You can then just next/next all the way through the rest of the installer wizard.

Install VS code (<https://code.visualstudio.com/download>):

It will make it easier if you set this as your preferred program for all available extensions & file types. You can then install some useful extensions by clicking the 5th icon from the top (Extensions) on the far left hand bar/pane and searching for them.

The ones that are most useful for ARMA stuff (for me) are:

- PowerShell (for script)
- SQF formatter
- SQF Language
- Arma 3 CfgFunctions

### Configure PowerShell, GIT and BUILD SCRIPT

Once git and VSCode are installed, hit Windows, search for and open "PowerShell" as ADMINISTRATOR (assuming your current user is an admin on your local machine)
replace relevant bits below with your username, password etc and copy & paste then run (enter):


```powershell
git config --global user.name "my_username"
git config --global user.email "my_email_123@gmail.com"
Set-ExecutionPolicy Unrestricted -Force -Confirm:$false
mkdir $profile.substring(0,($profile).LastIndexOf('\'))
New-Item $profile -Value @"
# e.g. '12.23.34.45'
$ENV:TOUR_SERVER_IP ='ENTER_TOUR_IP'
$ENV:TOUR_SERVER_PORT = 8821
# if you have single quotes (') in your password, you can swap it below for doubles (")
$env:TOUR_FTP_PASSWORD = 'MY_PASSWORD_FOR_CPDELUXE'
$env:TOUR_FTP_USERNAME = 'MY_USERNAME_FOR_CPDELUXE'
@"
```

## Per mission config

Below are the steps to initialise a mission folder with Git and add it to the Tour GitHub organisation.

### Initialise Git for your mission

Open PowerShell (can use VS Code integrated powershell terminal or default blue one) and run the below, making sure to:

- Ensure the $MissionFolderRoot actually points to the right folder and there is no trailing "\"
- Replace mission name as appropriate for your mission
- Ensure the $MissionFolderName does not have a version in! Be sure to leave the world name as it is (otherwise the ARMA editor will break)

```powershell
$MissionFolderRoot = 'C:\Users\my_windows_username\Documents\Arma 3 - Other Profiles\my_arma_username\missions'
$MissionFolderName = "30_tour_power_surge.Enoch"
cd "$MissionFolderRoot\$MissionFolderName"
git init
git add .
git commit -m "Initial commit"
# KEEP POWERSHELL WINDOW OPEN
```

### Add to GitHub organization

Steps:

- Go to the GitHub Organization (https://github.com/Tour-of-Teamrespawn) in your browser
- Click the _green_ NEW button, to create a new git repository
- Set the repository NAME to be the mission folder name (e.g. with example above: 30_tour_power_surge.Enoch)
- Ensure it is PUBLIC access (open source <3)
- Finish & create

You can then either:
- Copy commands from github page saying: "…or push an existing repository from the command line"

_OR_

- Run the below in your PS window from earlier to push your existing mission files to GitHub:

```powershell
git remote add origin https://github.com/Tour-of-Teamrespawn/$MissionFolderName.git
git branch -M main
git push -u origin main
```

If you refresh GitHub in your browser you should now see your code!
