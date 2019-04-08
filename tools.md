## Information gathering 

* exiftool
* [smtp-user-enum](http://pentestmonkey.net/tools/user-enumeration/smtp-user-enum)

## Password crack

* PSCredential: `powershell -c "$cred = Import-CliXml -Path cred.xml; $cred.GetNetworkCredential() | Format-List *"`
