# NOTEPAD

## SEQURITE ANTIVIRUS (SCREEN CASTING ISSUE)

1. edit Policy
2. Firewall -->> Exceptions --> Add
3. Name the Exception --> Protocol TCP ---> Application: ALL ---> Next
4. Select Direction: Inbound - Outbound Connnection  --> next
5. Local TCP/UDP Ports: All Ports --> Next
6. Remote IP Address: Any IP Address --> Next
7. Remote TCP/UTP Ports : All Ports --> Next
8. Action: Allow --> Finish

## or

All Same just on "first page" select Protocol "UDP" and Application: Specified Application Path --> C:\Windows\System32\WUDFHost.exe
