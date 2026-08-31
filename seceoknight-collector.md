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

