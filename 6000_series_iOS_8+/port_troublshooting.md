## Show/Clear Port Security Violations
```show port-security violation``` or ```show port-security shutdown```

### To Clear Violations and make changes (ver 8+)
- [ ] disable port to prevent immediate violation status ```interfaces <slot/port> admin-state disable```
- [ ] clear violations ```interfaces <slot/port> clear-violation-all```
- [ ] make changes
- [ ] enable port ```interfaces <slot/port> admin-state enable```

### Spantree Blocking
`show spantree ports blocking`
