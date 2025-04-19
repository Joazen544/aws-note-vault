將網域名稱和 [[IP address]]  相互映射的一個分散式資料庫，能夠使人更方便地訪問互連網，而不用去記住能夠被機器直接讀取的IP數串。
流程如下：
![[Pasted image 20250418151631.png]]
## Recursive Resolver
遞迴解析程式是回應來自用戶端之遞迴請求的電腦，並花時間追蹤 [DNS 記錄](https://www.cloudflare.com/learning/dns/dns-records/)。為執行此操作，其發出一系列請求，直到其到達所請求記錄的權威 DNS 名稱伺服器（或者逾時，或者如果未找到記錄，則傳回錯誤）。幸運的是，遞迴 DNS 解析程式並不總是需要發出多個請求才能追蹤回應用戶端所需的記錄；[快取](https://www.cloudflare.com/learning/cdn/what-is-caching/)是一種資料持久性過程，可透過在 DNS 查閱中更早地提供所請求的資源記錄，協助減少所需的請求數。
## Authoritative Nameserver
保留並負責處理 DNS 資源記錄的伺服器。這是位於 DNS 查閱鏈底部的伺服器，其將使用所查詢的資源記錄進行回應，從而最終允許發出請求的 Web 瀏覽器達到存取網站或其他網頁資源所需的 IP 位址。權威名稱伺服器可以透過自己的資料滿足查詢，不需要查詢另一個來源，因為這就是特定 DNS 記錄的事實最終來源。


## Attack
### DNS Spoofing
攻擊者通過偽造或篡改域名系統（DNS）的響應，誘導用戶訪問惡意或假冒的網站。例如，當你輸入「example.com」時，正常的DNS會返回真實的網站IP地址，但DNS欺騙可能返回一個假的IP地址，指向攻擊者的惡意網站。
* Solution: Domain Name System Security Extensions（DNSSEC）是一套用於增強域名系統（DNS）安全性的協議和技術。它通過數字簽名來驗證DNS數據的真實性和完整性，防止如DNS欺騙（DNS spoofing）或中間人攻擊等威脅。DNSSEC為DNS記錄添加加密簽名，確保用戶訪問的網站或服務是可信的，而不是被惡意篡改的。

### DNS快取投毒（DNS Cache Poisoning）
攻擊者向DNS解析器的快取中注入偽造的DNS記錄，導致後續查詢返回惡意IP地址。與DNS欺騙類似，但主要針對快取。
* ***DNSSEC（Domain Name System Security Extensions）**  
→ 用數位簽章驗證DNS回應，確保來源正確，防止偽造。
### 拒絕服務攻擊（DoS/DDoS）
攻擊者通過大量偽造的DNS請求淹沒DNS伺服器，使其無法正常回應合法請求，導致服務中斷。
* AWS Shield: 吸收大規模攻擊流量，保護DNS和其他網路服務。
### 中間人攻擊（Man-in-the-Middle Attack）
攻擊者在用戶與DNS伺服器之間攔截並篡改DNS查詢或響應，誘導用戶訪問惡意站點。
* ***DNS over HTTPS (DoH) / DNS over TLS (DoT)**  
→ 將DNS請求加密，防止被攔截和竄改。
### 域名搶註（Domain Name Hijacking）
攻擊者通過竊取域名註冊帳戶或偽造身份，修改域名的DNS配置，控制其解析指向。
- **域名鎖定（Domain Locking）**  
    → 開啟註冊商的「Registrar Lock」防止未經授權的變更。
    
- **啟用2FA和安全郵箱**  
    → 防止帳號被盜，保護你的域名管理權。
### **NXDOMAIN攻擊**  
攻擊者通過大量查詢不存在的域名（NXDOMAIN），耗盡DNS伺服器的資源，降低其性能。
**Rate Limiting + Query Filtering**  
→ 大型DNS服務如Cloudflare、Google DNS，會對異常查詢流量自動封鎖或限速。