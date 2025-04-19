A web service that speeds up distribution of your static and dynamic web content to your users. A Content Delivery Network (CDN) service
* It delivers your content through a worldwide network of data centers called **edge locations**. When a user requests content that you’re serving with CloudFront
	* 如果 cloudfront 有資料，馬上送
	* 沒有資料，先從 origin 拉，在送給 client （client 只會跟 cloudfront 拿資料）

## Components

![[Pasted image 20250419184530.png]]
### Original Server
S3 bucket or your own HTTP server, from which CloudFront gets your files which will then be distributed from CloudFront edge locations all over the world.

### Object
files to your origin servers.

### CloudFront Distribution
tells CloudFront which origin servers to get your files from when users request the files through your web site or application. At the same time, you specify details such as whether you want CloudFront to log all requests and whether you want the distribution to be enabled as soon as it’s created.

### edge locations
collections of servers in geographically dispersed data centers where CloudFront caches copies of your objects.

## Cache Strategy
Amazon CloudFront 的運作方式並不會自動將你上傳的靜態物件複製到**全世界的每個邊緣節點（Edge Location）**，而是根據**用戶的請求**和**緩存策略**來決定哪些邊緣節點會儲存該物件的副本。以下是具體的運作機制：

### Cache on Demand
- 當用戶請求一個物件（例如你上傳到 CloudFront 的靜態檔案）時，請求會被導向距離用戶最近的 CloudFront 邊緣節點。
- 如果該邊緣節點**已經緩存了這個物件**，則直接回傳給用戶，無需聯繫原始伺服器（例如 S3）。
- 如果該邊緣節點**沒有緩存該物件**，它會從**原始伺服器（Origin）**（如 S3 或其他後端）拉取該物件，儲存到該邊緣節點的緩存中，然後回傳給用戶。
- 這意味著，只有**實際有用戶請求的邊緣節點**才會拉取並緩存該物件，而不是全世界所有邊緣節點都會主動儲存。

### TTL 配置
- CloudFront 允許在分發設定中配置快取的 **最小 TTL (Minimum TTL)**、**最大 TTL (Maximum TTL)** 和 **預設 TTL (Default TTL)**，超過這個範圍就會重拉資料
- **最小 TTL**：即使來源伺服器指定短於此值的快取時間，CloudFront 也會至少快取此時間。
- **最大 TTL**：限制快取時間上限，即使來源指定更長時間。
- **預設 TTL**：當來源未提供 Cache-Control 或 Expires 時使用的預設快取時間。
- **常見設定**：靜態內容可能設定較高的預設 TTL（例如 24 小時），動態內容則設定為 0 或很短的時間。

##  **Performance and Availability**
### Origin Failover
負責主機壞掉的策略，需要建立一個 distribution 幫助 CDN 辨識目前的 original server 是誰
- The two origins in the origin group can be any combination of the following: AWS origins, like Amazon S3 buckets or Amazon EC2 instances, or custom origins, like your own HTTP web server.
- When you create the origin group, you configure CloudFront to failover to the second origin for GET, HEAD, and OPTIONS HTTP methods when the primary origin returns specific status codes that you configure.

## Security
- CloudFront, [AWS Shield](https://tutorialsdojo.com/aws-shield/), [AWS WAF](https://tutorialsdojo.com/aws-waf/), and Route 53 work seamlessly together to create a flexible, layered security perimeter against multiple types of attacks including network and application layer DDoS attacks.
- You can deliver your content, APIs or applications via SSL/TLS, and advanced SSL features are enabled automatically.
- - With **Origin Access Control (OAC)** feature, you can restrict access to an S3 bucket to only be accessible from CloudFront distributions. 確保只有透過 CloudFront 的請求才能存取來源內容
- - **Field-Level Encryption** is a feature of CloudFront that allows you to securely upload user-submitted data such as credit card numbers to your origin servers.這些欄位在傳輸到 CloudFront 邊緣節點後會被加密，只有最終的來源伺服器（或指定的後端服務）才能解密。