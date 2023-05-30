# Enabling PowerShell scripts execution in Windows 10/11

## Discription

The PowerShell Run Policy is a security feature that controls the conditions under which PowerShell loads configuration files and runs scripts. This feature helps prevent malicious scripts from running.

On a Windows computer, you can set the execution policy for the local computer, for the current user, or for a specific session. You can also use the Group Policy setting to set execution policies for computers and users.

Execution policies for the local computer and the current user are stored in the registry. You do not need to set execution policies in the PowerShell profile. The execution policy for a specific session is only stored in memory and is lost when the session is closed.

An execution policy is not a security system that restricts what users do. For example, users can easily bypass the policy by entering the contents of a script on the command line if they cannot run the script. Instead, an execution policy helps users set basic rules and prevents them from unintentionally violating them.

On computers other than Windows, the default - and Unrestricted - execution policy cannot be changed. The Set-ExecutionPolicy cmdlet is available, but PowerShell displays a console message that it is not supported. Although Get-ExecutionPolicy on Unrestricted platforms other than Windows, the behavior is actually the same because these platforms do not implement Windows Security zones.

## What is this for?

You may encounter security policy restrictions in Windows, for example when trying to activate the Python Virtual Environment.

To allow PowerShell scripts to run on Windows 10/11
## Method I (using PowerShell)

 - Run PowerShell as Administrator;
 - Set the scripts execution policy to one of the following states:

```powershell
Set-ExecutionPolicy remotesigned
```
or:
```
Set-ExecutionPolicy Bypass
```
You can also check the status of the current policies with the command:
```powershell
Get-ExecutionPolicy -List
```

## Method II (using Registry Editor)

```regfile
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\PowerShell]
"EnableScripts"=dword:00000001 "ExecutionPolicy"="Bypass"
```

```regfile
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\PowerShell]
"EnableScripts"=dword:00000001 "ExecutionPolicy"="Unrestricted"
```

### Execution Script without changes policy

You also execution your script on Local machine end-user apply next method:

```powershell
powershell.exe -noprofile -executionpolicy bypass -file .\Your_Script.ps1
```



You can read more  [here][MSDN-Ref]

[MSDN-Ref]: https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.3
