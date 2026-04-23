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

Cài đặt
Clone repository này:
git clone https://github.com/FlowerIF/ansibleLab.git
cd ansible-home-lab


Chạy và đưa ra kết quả
$ ansible-playbook -i inventory setup-server.yml --ask-vault-pass
Vault password: <xx>

PLAY [create centos with storage, user and cron] *******************************

TASK [Gathering Facts] *********************************************************

ok: [192.168.75.129]
ok: [192.168.75.128]

TASK [create part /dev/loop0] **************************************************

changed: [192.168.75.129]
changed: [192.168.75.128]

TASK [create PV] ***************************************************************

changed: [192.168.75.129]
changed: [192.168.75.128]

TASK [create LV 256M] **********************************************************

changed: [192.168.75.129]
changed: [192.168.75.128]

TASK [format lv xfs] ***********************************************************

changed: [192.168.75.129]
changed: [192.168.75.128]

TASK [create mount dir] ********************************************************

ok: [192.168.75.129]
ok: [192.168.75.128]

TASK [mount lv to dir] *********************************************************

[WARNING]: The value 0 (type int) in a string field was converted to '0' (type
string). If this does not look like what you expect, quote the entire value to
ensure it does not change.
changed: [192.168.75.129]
changed: [192.168.75.128]

TASK [create admin group] ******************************************************

ok: [192.168.75.129]
ok: [192.168.75.128]

TASK [create auto user with pass form vault] ***********************************

ok: [192.168.75.129]
ok: [192.168.75.128]

TASK [add admin group password less sudo] **************************************

ok: [192.168.75.129]
ok: [192.168.75.128]

TASK [add cron job auto delete logs at 2am] ************************************

[WARNING]: The value 2 (type int) in a string field was converted to '2' (type
string). If this does not look like what you expect, quote the entire value to
ensure it does not change.
ok: [192.168.75.129]
ok: [192.168.75.128]

PLAY RECAP *********************************************************************
192.168.75.128             : ok=11   changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
192.168.75.129             : ok=11   changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

