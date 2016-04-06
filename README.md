# DHCP
Sử dụng wireshark phân tích gói tin DHCP 

## I. Bắt gói tin 

Để bắt gói tin DHCP, trước tiên phải giải phóng IP: 

	> ipconfig /release

Sau đó bật Wireshark và cấp mới một địa chỉ IP

	> ipconfig /renew
	
<img src="http://i.imgur.com/YrRPcHG.png">

Ta sẽ bắt được 4 gói tin DHCP

<img src="http://i.imgur.com/V77th61.png"> 

## II. Phân tích gói tin 
### 1. DHCP Discover 

<img src="http://i.imgur.com/6ggIqYu.png">

- Client gửi thông điệp Discover theo hình thức Broadcast
-  IP nguồn 0.0.0.0, IP đích 255.255.255.255
- Cổng nguồn 68, cổng đích 67
- Opcode = 1 : Thông điệp yêu cầu
- Hardware type = 1 : Ethernet
- Transaction ID : 0xf084c8ea
- Flags==0 => đều tắt
- Các địa chỉ IP (Client IP Address, Your IP Address ) đặt mặc định là 0.0.0.0
- Các option : Type (discover), ClientID, Requested IP Address, host name, vendor classID, parameter request list.

### 2. DHCP Offer

<img src="http://i.imgur.com/YH1B5f0.png">
	
- Message type : 2 - thông điệp phản hồi 
- Địa chỉ cấp cho Client : 192.168.0.6
- Các option : Type(offer), ID server, IP address Lease Time, Subnet Mark, Router, DNS

### 3. DHCP Request

<img src="http://i.imgur.com/nrFlGKU.png">

- Client gửi thông điệp Discover theo hình thức Broadcast
- Cổng nguồn 68, cổng đích 67
- Opcode = 1 : Thông điệp yêu cầu
- Client IP, Your IP, Next server IP, relay agent IP : đặt về 0.0.0.0
- Các option : Type (resquest), ClientID, Requested IP Address, DHCP serverID, host name, Client fully qualified domain name, vendor classID, parameter request list.

### 4. DHCP Ack

<img src="http://i.imgur.com/d2Oj1Pf.png">

- IP nguồn : 192.168.0.1, IP đích 192.168.0.67
- Các option : Type (ACK), DHCP serverID, IP address Lease Time, Subnet Mark, Router, DNS