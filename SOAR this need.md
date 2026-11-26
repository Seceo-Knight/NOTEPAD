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

## To use this Playbook "Ransomware behaviour: shadow copies deleted".
We have to run this command on wazuh manager to create rule for SOAR

```
grep -rq 'id="100650"' /var/ossec/etc/rules/ && echo "STOP: 100650 already used" || { cat > /var/ossec/etc/rules/seceoknight_soar_rules.xml <<'EOF'
<group name="seceoknight_soar,ransomware,">
  <rule id="100650" level="14">
    <if_group>sysmon_event1</if_group>
    <field name="win.eventdata.commandLine" type="pcre2">(?i)(vssadmin(\.exe)?["\s]+(delete\s+shadows|resize\s+shadowstorage)|shadowcopy\s+delete|win32_shadowcopy.*(delete|remove)|bcdedit(\.exe)?.*recoveryenabled\s+no|wbadmin(\.exe)?["\s]+delete\s+(catalog|systemstatebackup|backup))</field>
    <description>Ransomware behaviour: backups or recovery being deleted on $(win.system.computer)</description>
    <mitre><id>T1490</id></mitre>
  </rule>
</group>
EOF
chown wazuh:wazuh /var/ossec/etc/rules/seceoknight_soar_rules.xml; chmod 660 /var/ossec/etc/rules/seceoknight_soar_rules.xml; systemctl restart wazuh-manager && sleep 15 && systemctl is-active wazuh-manager; grep -i "seceoknight_soar\|100650" /var/ossec/logs/ossec.log | tail -3; }
```
