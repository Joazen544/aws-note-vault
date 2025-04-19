![[Pasted image 20250418140757.png]]
本質上是一組運行在多個 AZ 的高可用性服務器，通過檢查應用層信息智能地分配流量，同時隱藏了後端架構的複雜性，為用戶提供單一接入點。

- operate at request level，檢查 url 路徑、host 跟 http 方法，將目標移到特定的 service (support routing)
- support instance, IP, lambda

* Request level ([[OSI Model#L7 The application layer]])
* Based on the content of requests
* Routing logic
	* path-based
	* host-based
	* query string parameter-based
	* source IP address-based
* Targets
	* Instances
	* IP addresses
	* Lambda functions
	* containers
* Network
	* Http
	* Https

