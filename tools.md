## Information gathering 

* exiftool
* [smtp-user-enum](http://pentestmonkey.net/tools/user-enumeration/smtp-user-enum)
* [icacls](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/icacls): Displays or modifies discretionary access control lists (DACLs) on specified files, and applies stored DACLs to files in specified directories.

## Password crack

* PSCredential: `powershell -c "$cred = Import-CliXml -Path cred.xml; $cred.GetNetworkCredential() | Format-List *"`
