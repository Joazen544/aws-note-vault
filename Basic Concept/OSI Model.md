
![[Pasted image 20250417210618.png]]
資料從上到下一層一層包起來，到了 server 再由下到上一層一層往上拆，一層只解一個。
在 Network 層主要的任務是把資料片段組成封包，並且透過 IP 在 router 管理封包的傳送。
#### L1 The physical layer
* Physical equipment
	* NIC
	* Port
	* cable
* Bits
#### L2 The data link layer
* Physical addressing
	* MAC
		* media access control address
		* MAC is connected to network interface card
	* MAC connect to Port
	* [[Ethernet protocol]] 
* Frames
#### L3 The network layer
* Path determination
	* [[IP adress]]
	* Routers
* Packets
#### L4 The transport layer
* End to end connections and reliability
	* TCP
		* Three-way handshake
	* UDP
	* TLS
* Segments
#### L5 The session layer
* Interhost communication
	* TCP
	* RPC
* Data
#### L6 The presentation layer
* Data representation and encryption
	* SSL
	* FTP
	* SSH
	* HTML
* Data
#### L7 The application layer
* Network services to end user applications
	* HTTP
	* FTP
	* SSH
	* DNS
* Data

