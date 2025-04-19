### 4/19
1. A company is building its customer web portal in multiple EC2 instances behind an Application Load Balancer. The portal must be accessible on [www.tutorialsdojo.com](https://tutorialsdojo.com/ "https://tutorialsdojo.com/") as well as on its [tutorialsdojo.com](https://tutorialsdojo.com/ "https://tutorialsdojo.com/") root domain. How should the Network Engineer set up Amazon Route 53 to satisfy this requirement?
a  Set up an Alias A Record for [tutorialsdojo.com](https://tutorialsdojo.com/ "https://tutorialsdojo.com") with the ALB as the target. For the [www.tutorialsdojo.com](https://tutorialsdojo.com/ "https://tutorialsdojo.com") subdomain, create a CNAME record that points to the ALB.
b. Set up a CNAME Record for [tutorialsdojo.com](https://tutorialsdojo.com/ "https://tutorialsdojo.com") with the ALB as the target. For the [www.tutorialsdojo.com](https://tutorialsdojo.com/ "https://tutorialsdojo.com") subdomain, create a CNAME record that points to the ALB.
c. Set up a CNAME Record for [tutorialsdojo.com](https://tutorialsdojo.com/ "https://tutorialsdojo.com") with the ALB as the target. For the [www.tutorialsdojo.com](https://tutorialsdojo.com/ "https://tutorialsdojo.com") subdomain, create an Alias A record that points to the ALB.
c. Set up a non-alias A Record for [tutorialsdojo.com](https://tutorialsdojo.com/ "https://tutorialsdojo.com") with the ALB as the target. For the [www.tutorialsdojo.com](https://tutorialsdojo.com/ "https://tutorialsdojo.com") subdomain, create a CNAME record that points to the ALB.

解答： A
* 解題要點：兩個 portal 都要能導向一個位置，一個是 sub domain, 一個是 host 
* 關聯概念: [[Route 53]] 的 resource record
* 詳解： 
	* [www.tutorialsdojo.com] 是 subdomain ，要倒向另一個 host 的話，要使用 cname 
	*  [tutorialsdojo.com] 是 root ，要倒向另一個host 必須使用 alias 


2. A Network Engineer has been tasked to protect the company’s publicly accessible online customer portal and to secure the clients’ sensitive financial information. Hackers must be prevented from intercepting DNS queries and from replacing the actual IP addresses of the website with unauthorized IP addresses in the DNS resolvers. The solution should protect the users from being routed to the IP addresses provided by the attackers in the spoofed response that could potentially direct them to fake or phishing websites.

What should the Engineer do to satisfy this requirement?

1. Enable Domain Name System Security Extensions (DNSSEC) in Amazon Route 53.
2. Enable Server Name Indication (SNI) in Amazon Route 53.
3. Set up a private hosted zone in Amazon Route 53 and launch a BIND DNS Server.
4. Set up Perfect Forward Secrecy (PFS) using Diffie-Hellman (DH) group 2 to prevent DNS spoofing.
解答： 1.
* 關鍵字：DNS spoofing
* 關聯概念: [[Route 53]] 的 resource record, [[DNS]] 
* 詳解：
	* **Spoofing**: 利用假回應誘導使用者去其他網頁，DNSSEC 可以使用數位簽章避免偽造
	* **Server Name Indication (SNI)**：如果很多網頁都綁在同一個 ip ， server 容易不知道該用哪一個 key 給 client 。SNI 是 **TLS（傳輸層安全協議）** 的一個擴展。SNI 允許一台伺服器在同一個IP上，根據客戶端請求的「主機名稱」來決定回應哪張 SSL/TLS 。
	* **BIND SERVER**: BIND 是全球最常用的DNS伺服器，功能完善，支援 ACL 防火牆
	* **Perfect Forward Secrecy**: 每次連線時，都用**臨時密鑰**（Session Key），而且這個密鑰：不存檔、不重複使用。即使伺服器私鑰被盜，也無法回頭解密舊資料。


