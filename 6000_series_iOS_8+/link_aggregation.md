# LACP (dynamic) [2 linkagg with 2 ports]
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
# Static
```
static linkagg 1 size 2 name "<name>" admin state enable
```
