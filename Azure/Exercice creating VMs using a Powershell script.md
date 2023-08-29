# Creating the script:
## Powershell scripting basics:
**To access parameters within a script we use :**
`param([string]$resourceGroup)`  
the parameter in name matched if not in order, if in order it is type matched.

**To assign a variable we do :**
`$Variable = Value | Cmdlet`

**To make for loops we do:**
```
For ($i = 1; $i -le 3; $i++) 
{

}
```
**Conditional statements are done using :**
-lt : less than, -eq: equals ...

## Final script:
```
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    New-AzVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image Canonical:0001-com-ubuntu-server-focal:20_04-lts:latest
}
```

**To run this script we use :**
`./ConferenceDailyReset.ps1 learn-97f16455-5c11-4fce-bbf7-a0b74717cd18`