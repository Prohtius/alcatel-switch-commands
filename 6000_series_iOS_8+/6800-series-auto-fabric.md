# 6800 Series
## Disable Auto Fabric

>[!IMPORTANT]
>Disabling Auto Fabric should be done the first time the switch is started before any other configuration changes.

>[!WARNING]
>Auto fabric should only be disabled if it is not going to be used.

```
reload from working no rollback-timeout
auto-fabric admin-state enable
mvrp enable
no virtual-chassis auto-vf-link-port 1/1/53
no virtual-chassis auto-vf-link-port 1/1/54
auto-fabric protocols lacp admin-state disable
auto-fabric protocols ip all admin-state disable
auto-fabric protocols mvrp admin-state disable
auto-fabric protocols spb admin-state disable
auto-fabric interface 1/1/1-54 admin-state disable
mvrp disable
spb isis admin-state disable
no spb bvlan 4000-4015
spantree mode per-vlan
auto-fabric admin-state disable remove-global-config
auto-fabric admin-state disable
Copy running certified
write memory flash-synchro
reload all
```
