```
failover peer “failover-dhcp” {
  primary;
  address 172.16.1.10:;
  port 847;
  peer address 172.16.1.11;
  peer port 647;
  max-response-delay 180;
  mclt 1800;
  split 128;
  load balance max seconds 3;
}
subnet 172.16.1.0 netmask 255.255.255.0 {
        option routers 172.16.1.2;
        option subnet-mask 255.255.255.0;
        option domain-search "final.local";
        option domain-name-servers 172.16.1.12, 172.16.1.13;
        max-lease-time 12600;
        default-lease-time 3600;
        pool {
              failover peer "failover-dhcp":
              range 172.16.1.100 172.16.1.150;
        }
}
```
