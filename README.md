# Alcatel Switch Commands

## Clear certified mode
`copy certified working make-running-directory`

## Save Commands
### Pre ver. 8
```
copy running-config working
copy working certified
write memory flash-synchro
```
### Ver 8+
```
copy running certified
copy certified working
write memory flash-synchro
```
## DHCP Relay (ver 8+)
```
ip dhcp relay interface <interface name> destination <dhcp server ip address>
```
## Port Troubleshooing
### Violations
`show port-security violation`
`show port-security shutdown`

#### To Clear Violations and make changes (ver 8+)
`interfaces <slot/number> admin-state disable` <br/>
`interfaces <slot/port> clear-violation-all` <br/>

make changes then enable port again <br/>
`interfaces <slot/number> admin-state enable`

### Spantree Blocking
`show spantree ports blocking`

## Multicast Commands
```
ip multicast status disable
ip multicast querying disable

ip multicast querier-forwarding disable
ip multicast vlan 100 status disable
ip multicast vlan 702 status disable
ip multicast vlan 998 status disable
ip multicast vlan 100 querier-forwarding disable
ip multicast vlan 702 querier-forwarding disable
ip multicast vlan 998 querier-forwarding disable
```
## Link Agg Commands
### Create Link Agg
#### lacp (dynamic) [2 linkagg with 2 ports]
```
    lacp linkagg 1 size 2 name "<name>" admin state enable
    lacp linkagg 2 size 2 name "<name>" admin state enable

    lacp linkagg 1 actor admin key 1
    lacp linkagg 2 actor admin key 2

    lacp agg 1/4 actor admin key 1
    lacp agg 1/5 actor admin key 1
    lacp agg 1/19 actor admin key 2
    lacp agg 1/20 actor admin key 2    

    vlan <vlan> port default 1
    vlan <vlan> port default 2
```
#### static
```
    static linkagg 1 size 2 name "<name>" admin state enable
```
## Port Security
```
port-security port 1/1/11 maximum 3
port-security port 1/1/11 learn-trap-threshold 3
port-security port 1/1/11 admin-state enable
```
