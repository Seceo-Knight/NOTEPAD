if audit is desable in windows server then do this to enable it 

1. first open cmd as admin and then. so we can able to use this SOAR policy "Windows password attack or lockout"
```
auditpol /set /subcategory:"Logon","Account Lockout" /success:enable /failure:enable
```
