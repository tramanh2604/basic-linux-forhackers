# Chapter 4: Adding & removing software
- Có cách để thêm phần mềm:
	+ apt package manager
	+ GUI-based installation managers
	+ git

## 1. Dùng apt

**Note: các lệnh apt-get có thể đc viết dưới dạng apt trừ lệnh apt-cache**

### 1.1 Tìm package
- Trước khi download, check xem package có nằm trong reposotory hay không bằng lệnh: `apt-cache search [keyword]`

### 1.2 Thêm phần mềm
- Lệnh: `apt-get install [packagename]`

### 1.3 Xóa phần mềm
- Lệnh: `apt-get remove [packagename]`
- Lệnh này chỉ gỡ phần mềm, k xóa configuration files, có thể reinstall package lại lần sau nếu muốn.

- Lệnh: `apt-get purge [packagename]`
- Gỡ phần mềm và xóa cả configuration files.

### 1.4 Updating package
- Update là cập nhật danh sách package có sẵn trong repository, không cài đặt hay nâng cấp bất kì phần mềm nào.
- Upgrade: tải và cài đặt phiên bản mới nhất của phần mềm (the lastest version).
- Lệnh update: `apt-get update`

### 1.5 Upgrading Package
- Để nâng cấp (upgrade) package đã có sẵn, dùng lệnh: `sudo apt-get upgrade`. Lệnh này sẽ upgrade tất cả các package có sẵn trong repository.

## 2. Thêm repository vào sources.list file
- Ví dụ Kali repository chứa rất nhiều software về security và hacking, nên nó k chứa những phần mềm hoặc tool các phần mềm thông thường => nên add thêm backup repository để system có search các case trong trường hợp k có trong Kali repository.
- Repository nằm ở *sources.list* tại */etc/apt/sources.list* và có thể mở bằng text editor. 
	+ Ví dụ mở bằng nano, dùng lệnh: `nano /etc/apt/sources.list`.
	+ Thêm tên của repository rồi save.
- Không thêm các unstable repository vào sources.list -> problematic for your system.

## 3. Dùng GUI-based installer
- New version của KAli có đi kèm một GUI-based software installer tool nhưng cần cài đặt các GUI này trước bằng `apt-get`.
- 2 GUI phổ biến là Synaptic và Gdebi.
- Ví dụ cài Synaptic, dùng lệnh: `apt-get install synaptic`
- Sau khi install, **Settings -> Synaptic Package Manager**, open a window như sau:

![synaptic](/images/synaptic.PNG)

- **Search:** tìm kiếm package.
- Checkbox vào phần mềm muốn download rồi nhấn **Apply**.

## 4. Dùng git
- Thỉnh thoảng 1 số phần mềm k có trong bất kỳ repository nào, có thể có trên github.
	|Ví dụ muốn *bluediving* (a bluetooth hacking and pentesting suite), k tìm thấy trên Kali có thể search trên github trước. 
- Một khi tìm thấy phần mềm trên github muốn cài đặt, dùng lệnh `git clone [URL]`.
	| Ví dụ: `git clone https://github.com/balle/bluediving.git`.
	+ Sau đó kiểm tra lại bằng `ls -l`
	+ Nếu thấy bluediving /hoom thì là thành công.