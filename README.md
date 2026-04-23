Ansible Home Lab - Tự động hóa cấu hình server CentOS
Sử dụng Ansible để tự động cấu hình một server chạy CentOS 8/9 hoặc Rocky Linux, bao gồm thiết lập LVM storage,
quản lý user với quyền sudo không cần mật khẩu, và tạo cron job định kỳ.


Tính năng
LVM Storage:
Tạo loop device, thiết lập physical volume, volume group, logical volume (256MB),
format với hệ thống file XFS, và mount cố định vào thư mục /opt/app.
User & Sudo:
Tạo user automate với mật khẩu đã được hash (lưu trong Ansible Vault) 
và thêm vào group admin với quyền sudo không cần nhập mật khẩu.
Cron Job:
Thiết lập job xoay vòng log mỗi ngày lúc 2 giờ sáng bằng logrotate.


Yêu cầu
Control node:
Máy Linux có cài Ansible (ansible-core phiên bản 2.13 trở lên)
Managed node:
Server chạy CentOS 8/9 hoặc Rocky Linux 8/9, có Python 3, cho phép SSH bằng root (lab sử dụng sshkey)
Ansible Vault:
Dùng để mã hóa mật khẩu user
