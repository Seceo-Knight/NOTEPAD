At this point, I recommend not changing the existing Wazuh default Rule 594. We can use local_rules.xml to reduce the noise safely.

```nano /var/ossec/etc/rules/noise_reduction.xml```

```
<group name="local,syscheck,">

  <rule id="100830" level="1">
    <if_sid>594</if_sid>
    <match>Changed attributes: mtime</match>
    <description>Registry mtime-only change downgraded from Rule 594</description>
  </rule>

</group>
```

Tunning False positive rule please add this in local_rules.xml
```
<group name="local,sysmon,">
  <rule id="100961" level="0">
    <if_sid>61618</if_sid>
    <field name="win.eventdata.image" type="pcre2">(?i)^c:\\{1,2}windows\\{1,2}system32\\{1,2}svchost\.exe$</field>
    <field name="win.eventdata.commandLine" type="pcre2">(?i)svchost\.exe\S*\s+-k\s+\w+</field>
    <field name="win.eventdata.user" type="pcre2">(?i)^nt authority\\{1,2}(system|local service|network service)$</field>
    <description>svchost.exe started as a normal Windows service (parent missing in the Sysmon event): not suspicious</description>
  </rule>
</group>
```
Make Firewall interface login rule id 81626 to rule level 12 to detect in AI

```
grep -rn "81626" /var/ossec/ruleset/rules/
```
then nano it and make this rule id to level 12


-------------------------

make ssh bruteforce attack to level 12 
```
nano /var/ossec/ruleset/rules/0095-sshd_rules.xml
```
then change rule level for rule id's - 5712 and 5763
