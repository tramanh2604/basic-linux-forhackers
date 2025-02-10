# CHAP 3: ANALYZING & MANAGING NETWORKS

## 1. Analyzing networks with ifconfig

![ifconfig](/images/ifconfig.png)

- ifconfig dùng để kiểm tra và tương tác với các giao diện mạng của hệ thống

1) eth0: EthernetO. Mạng có dây đầu tiên đang đc kết nối (wired network connection). Nếu có nhiều mạng đang đc kết nối hơn thì format thể hiện là eth1, eth2...

Loại mạng đang đc dùng cũng đc liệt kê (ethernet), HWaddr và đchỉ - NIC/MAC.

2) IP address

3) Broadcast address, dùng để gửi data tới tất cả IP trên cùng 1 subnet.

4) network mask: xác định phần nào của đchi IP đc dùng để kết nối vs local network.

5) lo: localhost. Đchi của 1 special software kết nối vs hệ thống của chính bạn.

6) wlan0: chỉ xuất hiện nếu có wireless interface hoặc adapter. 

=> ifconfig cho phép bạn kết nối và thao tác trên cài đặt LAN.

## 2. Kiểm tra các thiết bị mạng k dây với iwconfig

- Có thể dùng iwconfig để thu thập các thông tin cần thiết cho cuộc tấn công mạng k dây như địa chỉ IP của adapter, MAC, model...

![iwconfig](/images/iwconfig.PNG)

1) wlan0: mạng k dây duy nhất, theo chuận 820.11 IEEE, băng tần b và g (2 tiêu chuẩn băng tần ban đầu). Hầu hết các thiết bị k dây hiện nay có cả n (chuẩn mới nhất).

2) Mode của wlan0 là Managed, còn có mode moniter và promiscous. Cần mode là promiscuous để cracking wireless password.

3) Not Associated: wireless adapter k đc kết nối với AP

4) Công suất là 20 dBm - đại diện cho cường độ tín hiệu.

## 3. Thay đổi thông tin network
- Giúp kết nối với các network khác dưới dạng trusted device. Ví dụ trong DOS attack, bạn có thể làm giả đchi IP (spoofing IP) để attack đến từ nguồn khác, tránh đc forensic analyst.

### 3.1 Thay đổi đchi IP
- Để thay đổi đchi IP, dùng lệnh `ifconfig eth0 đchIP`
- Ví dụ để gán đchi IP 192.168.181.115 cho interface ta dùng lệnh: `ifconfig eth0 192.168.181.115`. Nếu thực hiện đúng, k trả kết quả.
- Check network lại với ifconfig, ta thấy đchi IP thay đổi thành IP mới ta vừa gán.

### 3.2 Thay đổi đchi Mask và Broadcast
- Ví dụ muốn gán eth0 với netmask là 255.255.0.0 và broadcast là 192.168.1.255 ta dùng lệnh
`ifconfig eth0 192.168.181.115 netmask 255.255.0.0 broadcast 192.168.1.255`

### 3.3 Spoofing MAC address
- Có thể dùng ifconfig để đổi đchi MAC hoặc HWaddr. MAC là đchi duy nhất và thường đc dùng cho mục đích bảo mật như chặn hacket khỏi network và theo dõi. 
- Thay đổi đchi MAC là cách hữu ích để vượt qua kiểm soát truy cập mạng.
```
ifconfig eth0 down

 ifconfig eth0 hw ether 00:11:22:33:44:55
 
 ifconfig eth0 up
```

- Dùng command down để xem giao diện interface (eth0). hw (hardware) và ether (ethernet) và đchi MAC giả mạo. Cuối cùng là backup interface với up option để thay đổi.

### 3.4 Gán đchi IP mới từ DHCP Server
- Linux có DHCP chạy tiến trình ngầm (daemon), gọi là *dhcpd*. DHCP server gán đcho IP cho tất cả system trong subnet và keep log file có đchi IP đc gán cho các máy tại cùng 1 thời điểm. 
- Khi kết nối internet từ LAN, phải có DHCP gán IP. Do đó, sau khi đặt đchi IP tĩnh, phải quay lại và nhận IP mới đc DHCP chỉ định. Để làm đc điều này, phải khởi động lại hệ thống. 
- Để request IP từ DHCP, gọi DHCP bằng command `dhclient eth0`  
- Sau đó dùng *ifconfig* sẽ thấy DHCP đã gán 1 IP mới, 1 broadcast mới và 1 netmask mới cho eth0

## 4. Thao tác với Domain Name System (hệ thống tên miền)
- Hackers có thể tìm thấy nhiều data về mục tiêu trong DNS. DNS dùng để chuyển đổi tên miền thành IP, hacker có thể dùng nó để thu thập data.

### 4.1 Kiểm tra DNS với dig
- Thông tin thu thập từ DNS có thể là target's nameserver, target's email server, subdomains, IP addresses...

- Using dig and ns option để nhận infor về domain nameserver. `dig hackers-arise.com ns`

![dig](/images/dig.PNG)

+ *ADDITIONAL SECTION* trả đchi IP (216.239.32.100) của DNS server phục vụ *hackers-arise.com*
+ *mx* option: get infor về email server kết nối vs domain.

### 4.2 Thay đổi DNS server
- Nếu muốn thay đổi DNS server, chỉnh sửa filename */etc/resolv.conf*. 
- Ví dụ dùng nano để chỉnh sửa: `nano /etc/resolv.conf`

![resolv.conf](/images/resolv-conf.PNG)

+ nameserver được set tới local DNS server có đchi 192.168.181.2. Ví dụ muốn thay đổi nameserver thành Google's DNS server có đchi 8.8.8.8 => sửa rồi save

## 5. Mapping your own IP addresses
- The host file: chuyển đổi tên miền -> IP. The hosts file nằm ở */etc/hosts*, bạn có thể tạo ra IP - domain name mapping. Ví dụ, quyết định đchi của browser khi truy cập www.google.com. Hacker có thể chiếm quyền đkhiển kết nối TCP trên mạng cục bộ để hướng lưu lượng truy cập tới các webserver độc hại bằng tool *dnnspoof*

- Dùng lệnh `nano /etc/hosts`

![hosts file](/images/hosts-file.PNG)

+ By default, the hosts file chỉ chứa mapping cho localhost tại 127.0.0.1, và system's hostname tại 127.0.1.1
+ Có thể thêm bất kỳ IP nào nối với bất kì domain bạn muốn. Ví dụ `192.168.181.131	bankofamerica.com`
+ Nhớ tab giữa IP và domain.
