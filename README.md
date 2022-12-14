# Unprotect DMaaS M365 OneDrives using PowerShell
Warning: this code is provided on a best effort basis and is not in any way officially supported or sanctioned by Cohesity. The code is intentionally kept simple to retain value as example code. The code in this repository is provided as-is and the author accepts no liability for damages resulting from its use.

This powershell script removes protection for DMaaS M365 OneDrives. This script was created for the purpose of automating the offboarding of M365 users. 

Download the script
Run these commands from PowerShell to download the script(s) into your current directory

~~~
# Download Commands
$scriptName = 'UnprotectDmaasM365OneDrives' 
$repoURL = 'https://raw.githubusercontent.com/danfrankenstein/UnprotectDMaaSM365OneDrives/main' 
(Invoke-WebRequest -UseBasicParsing -Uri "$repoUrl/$scriptName.ps1").content | Out-File "$scriptName.ps1"; (Get-Content "$scriptName.ps1") | Set-Content "$scriptName.ps1" 
(Invoke-WebRequest -UseBasicParsing -Uri "$repoUrl/cohesity-api.ps1").content | Out-File cohesity-api.ps1; (Get-Content cohesity-api.ps1) | Set-Content cohesity-api.ps1
# End Download Commands
~~~

# Components
*protectDmaasM365OneDrives.ps1: the main powershell script
*cohesity-api.ps1: the Cohesity REST API helper module
Place both files in a folder together and run the main script like so:
~~~
./unprotectDmaasM365onedrives.ps1 -region us-east-2 `
                                -sourceName mydomain.onmicrosoft.com `
                                -users user1.mydomain.onmicrosoft.com, user2.mydomain.onmicrosoft.com, Display Name `
                                -userList ./userlist.txt
~~~
# Parameters

- -username: (optional) used for password storage only (default is 'DMaaS')
- -region: DMaaS region to use
- -sourceName: name of registered M365 protection source
- -users: (optional) one or more OneDrives "display names" or SMTP addresses (comma separated)
- -userList: (optional) text file of OneDrive names or SMTP addresses (one per line)
- -pageSize: (optional) limit number of objects returned pr page (default is 50000)

# Authenticating to DMaaS

DMaaS uses an API key for authentication. To acquire an API key:

- log onto DMaaS
- click Settings -> access management -> API Keys
- click Add API Key
- enter a name for your key
- click Save

Immediately copy the API key (you only have one chance to copy the key. Once you leave the screen, you can not access it again). When running a DMaaS compatible script for the first time, you will be prompted for a password. Enter the API key as the password.# UnprotectM365OneDrives
 
