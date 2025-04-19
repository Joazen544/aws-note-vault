![[Pasted image 20250418140934.png]]
在 TCP 層面運作，不查看請求內容，並維持連接的原始源 IP 地址
- high performance / low latency
**應用場景：**
- **需要極低延遲和高吞吐量**：金融交易、遊戲服務器、實時通訊
- **非 HTTP/HTTPS 協議**：
    - MQTT（物聯網）
    - 遊戲協議
    - 自定義 TCP 協議

* Connection Level ([[OSI Model#L4 The transport layer]]) TCP, UDP
* Based on IP protocol data
* High performance, low latency, [[TLS offloading at scale]]
* Can have static IP / Elastic IP
* Targets
	* UDP
	* Static IP addresses

