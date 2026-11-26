if audit is desable in windows server then do this to enable it 

1. first open cmd as admin and then. so we can able to use this SOAR policy "Windows password attack or lockout"
```
auditpol /set /subcategory:"Logon","Account Lockout" /success:enable /failure:enable
```
2. for windows password attack or lockout SOAR playbook we have to enable it as well for lockout for 5 min. on server
Run this in cmd as a admin
```
net accounts /lockoutthreshold:5 /lockoutduration:5 /lockoutwindow:5
```
