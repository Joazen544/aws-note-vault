
![[Pasted image 20250418141525.png]]

* A highly available and scalable Domain Name System (DNS) web service used for domain registration, DNS routing, and health checking.
* The service automatically makes itself the DNS service for the domain by doing the following:
## Components 
### Routing Traffic

![[Pasted image 20250418142952.png]]
	- Creates a hosted zone that has the same name as your domain.
	- Assigns a set of four name servers to the hosted zone. When someone uses a browser to access your website, such as www.example.com, these name servers tell the browser where to find your resources, such as a web server or an S3 bucket.
	- Gets the name servers from the hosted zone and adds them to the domain.

### Health Checks
- Create a health check and specify values that define how you want the health check to work, such as:
    - The IP address or domain name of the endpoint that you want Route 53 to monitor.
    - The protocol that you want Route 53 to use to perform the check: HTTP, HTTPS, or TCP. ([[OSI Model]])
    - The **request interval** you want Route 53 to send a request to the endpoint.
    - How many consecutive times the endpoint must fail to respond to requests before Route 53 considers it unhealthy. This is the **failure threshold**.
- You can configure a health check to check the health of one or more other health checks.
- You can configure a health check to check the status of a CloudWatch alarm so that you can be notified on the basis of a broad range of criteria.

## Resource Record
DNS server 內紀錄資源的檔案
### CNAME Record
**想要在子網域（**www.example.com**）** 指向另一個網域（而不是 IP）
全名是 **Canonical Name Record**，用來把一個網域名稱 **別名** 指向另一個「正確的、實際的」網域名稱。
查詢對象為子網域（例如 foo.example.com 或 [blog.cloudflare.com](https://blog.cloudflare.com/)）的情況下，將向權威名稱伺服器之後的序列新增一個附加名稱伺服器，其負責儲存該子網域的 [CNAME 記錄](https://www.cloudflare.com/learning/dns/dns-records/dns-cname-record/)。
### Alias Record 
**想要在根網域（**example.com**）** 也能指向另一個網域（而不是 IP）
當您要將主域名 (不是子網域)「指向」主機名稱時，就可以使用 ALIAS 紀錄。
ALIAS 紀錄有點像 [CNAME 紀錄](https://docs.gandi.net/zh-hant/domain_names/faq/record_types/cname_record.html#cname-records) ，但當您要將主網域指向主機名稱而不是 IP 位址時，就必須使用 ALIAS 紀錄。由於您無法在主域名上使用 CNAME 紀錄，所以使用 ALIAS 紀錄是最好的解決方法。

![[Screenshot 2025-04-18 at 3.47.01 PM.png]]
• **要轉向其他網域，且是在子網域用，就用** CNAME
• **如果是根網域（**example.com**），又不想硬寫 IP，那就用** ALIAS **或服務商提供的特殊功能**


## Routing Policy
* **Simple Routing Policy**: route internet traffic to a single resource that performs a given function for your domain.
*  **Failover routing policy** – use when you want to configure active-passive failover.
* **Geoproximity routing policy** – use when you want to route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another.
* **Latency routing policy** – use when you have resources in multiple locations and you want to route traffic to the resource that provides the best latency.
##  **Health Checks and DNS Failover**
- Each health checker evaluates the health of the endpoint based on two values:
    - Response time
    - Whether the endpoint responds to a number of consecutive health checks that you specify (the failure threshold)
- Types of health checks
	- **HTTP and HTTPS health checks** –  establish a TCP connection with the endpoint within four seconds.
	- **TCP health checks** – establish a TCP connection with the endpoint within ten seconds.
	- **HTTP and HTTPS health checks with string matching** - establish a TCP connection with the endpoint within four seconds, and the endpoint must respond with an HTTP status code of 2xx or 3xx within two seconds after connecting.

- Two types of failover configurations
    - **Active-Active Failover** – 
	    - 多個資源 **同時上線**，所有健康的都可以回應
	    - 每個資源都會做健康檢查
	    - all the records that have the same name, the same type, and the same routing policy are active unless Route 53 considers them unhealthy. 
    - **Active-Passive Failover** – 
	    - 只有 **主資源上線**，備援資源待命
	    - 主資源與備援資源都會做健康檢查，但預設只使用主資源
	    - use this failover configuration when you want a primary resource or group of resources to be available the majority of the time and you want a secondary resource or group of resources to be on standby in case all the primary resources become unavailable. 