192.168.0.1

Ip addresses are written in dotted decimal notation
Each part of the address is a binary octet

IP 位址是一串 32 位元的數字。 該位址會獨一無二地識別 TCP/IP 網路上的主機。 在網路之間傳送資料封包的 Router，並不知道資訊封包目的地之主機的確切位置。 路由器只會知道主機所屬的網路，並且會利用儲存在其路由表中的資訊，來決定如何將封包傳送到目的地主機的網路。 當封包傳送到目的地網路之後，該封包就會傳送到適當的主機。

1. **發送端(本地網路內部)**:
    - 你的裝置(如手機，電腦)使用私有IP位址(如192.168.1.5)
    - 當你的裝置要發送資料到網際網路上的伺服器時
2. **經過發送端路由器**:
    - 資料包首先發送到你的路由器
    - 路由器執行網路位址轉換(NAT)，將資料包的來源位址從私有IP(192.168.1.5)更改為路由器的公網IP(例如203.0.113.1)
    - 路由器記住這個連接，以便知道返回的資料應該發送給哪個內部裝置
3. **網際網路傳輸**:
    - 資料包通過網際網路傳輸，使用公網IP位址進行路由
    - 資料包最終到達目標伺服器所在的網路
4. **接收端網路**:
    - 如果目標是另一個家庭/辦公室網路中的裝置，則該網路的路由器接收資料包
    - 接收端路由器根據NAT表或埠轉發規則，決定將資料包轉發給內部網路中的哪個私有IP位址
    - 資料包最終到達目標裝置