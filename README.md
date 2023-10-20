# RPR RPR+ SSO

Redundant supervisor modules can be configured in several modes. The redundancy mode affects how the two supervisors handshake and synchronize information. Also, the mode limits the state of readiness for the standby supervisor. The more ready the standby module is allowed to become, the less initialization and failover time will be required.

L2 Redundancy Mode

1. Route Processor Redundancy (RPR):  Standby module reloads every other module, initializes all supervisor functions. failover time <2 minutes

2. Route Processor Redundancy Plus (RPR+): Standby module finishes initializing without reloading other modules. failover time<30 seconds

3. Stateful Switchover (SSO): - Standby module is already initialized. failover time < 1 second.
   SSO allows for Cisco Nonstop Forwarding.


L3 Redundacy Mode

1. Cisco NonStop Forwarding (NSF)

You can enable another redundancy feature along with SSO. Cisco Nonstop Forwarding (NSF) is an interactive method that focuses on quickly rebuilding the Routing Information Base (RIB) table after a supervisor switchover. The RIB is used to generate the Forwarding Information Base (FIB) table for Cisco Express Forwarding, which is downloaded to any switch module that can perform Cisco Express Forwarding.

## Configuration RPR, RPR+, SSO

For RPR: Router(config-r)#mode rpr
For RPR+: Router(config-r)#mode rpr-plus
For SSO: Router(config-r)#mode sso

1. Configure the Primary Route Processor:
```
Router#configure terminal
Router(config)#redundancy
Router(config-r)#mode rpr
```
2. Check the Configuration:
```
Router#show running-config
```
3. Save the Configuration:
```
Router#copy running-config startup-config
```
4. Configure the Secondary Route Processor:
```
Router-Standby#configure terminal
Router-Standby(config)#redundancy
Router-Standby(config-r)#mode rpr
```
5. verify configuration
```
Router# show running-config
Router# show redundancy states
```

## Configuration NSF

for note, NSF only work on Dynamic routing and in SSO.
you configured in inside the routing commands:

```
Router(config)#router ospf 1
Router(config-router)#nsf
```
To enable NSF for IS-IS:
```
Router(config)#router isis
Router(config-router)#nsf
```
And to enable NSF for BGP:
```
Router(config)#router bgp 65000
Router(config-router)#bgp graceful-restart

```


