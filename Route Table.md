Route Table 決定往特定網段 (Destination) 的封包怎麼走 (Target) 常見 Target 有：

- local
- NAT Portal
- igw (internet gateway)
- vgw (virtual gateway) 用於串接企業內部 vpn 每個 subnet 只能指定零或一張 routing table 有一張 route table 可以設為預設；未指定的 subnet 都參照它 (main) 每個 subnet 的 CIDR 區塊不能重疊，不能大於 VPC。 支援 IPv6 提供 ACL，但通常預設夠用。