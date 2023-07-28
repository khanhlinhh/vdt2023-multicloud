# Migration Tool 
## 1. OS Migrate

>[Github](https://github.com/os-migrate/os-migrate) 
>47 ★ </br>
>Cập nhật lần cuối: 1 tuần trước </br>
>[os-migrate documentation](https://os-migrate.github.io/os-migrate/index.html)

``` bash
docker pull ghcr.io/os-migrate/os-migrate/os_migrate_toolbox:main
```

Hộp công cụ mã nguồn mở giúp di chuyển song song giữa các đám mây OpenStack. Di chuyển song song trên đám mây là một cách để hiện đại hóa việc triển khai OpenStack. Thay vì nâng cấp cụm OpenStack tại chỗ, cụm OpenStack thứ hai được triển khai cùng với dữ liệu của tenant được di chuyển từ cụm ban đầu sang cụm mới. Khi tài nguyên phần cứng giải phóng trong cụm cũ, chúng có thể được thêm dần vào cụm mới. 

OS Migrate cung cấp một framework để export và import tài nguyên giữa hai đám mây - bộ sưu tập các playbook Ansible cung cấp chức năng cơ bản, nhưng **có thể không phù hợp với từng trường hợp sử dụng cụ thể**. Playbook có thể được **tùy chỉnh** bằng cách sử dụng các phần của OS Migrate collections (roles và modules) làm building blocks. 

OS Migrate sử dụng API OpenStack chính thức một cách nghiêm ngặt và không sử dụng quyền truy cập cơ sở dữ liệu trực tiếp hoặc các phương pháp khác để xuất hoặc nhập dữ liệu. Playbook Ansible có trong OS Migrate là bình thường.

## 2. Cyclone

>[Github.](https://github.com/sapcc/cyclone) </br>
>10 ★ </br>
>Cập nhật lần cuối: 1 tháng trước

Cyclone (Cloud Clone hoặc cclone) giúp di chuyển (migrate) hoặc sao chép (clone) nó sang một OpenStack region mới hoặc Availability Zone. Cyclone quan tâm đến tất cả các volumes được đính kèm với VM và sao chép chúng với tất cả các chuyển đổi type trung gian bắt buộc.

Di chuyển volume được thực hiện bằng cách chuyển đổi volume thành image rồi migrate image giữa các region, sau đó chuyển đổi image trở lại thành volume. Di chuyển volumes trong cùng region được thực hiện bằng phương pháp [Volume Transfer](https://docs.openstack.org/cinder/latest/cli/cli-manage-volumes.html#transfer-a-volume).

→ Lưu ý về hạn ngạch (quota), đặc biệt là quote của dự án nguồn, khi clone một volume. Nó yêu cầu gấp đôi quota kích thước volume Cinder (Block Storage). Nếu cờ `--clone-via-snapshot` được chỉ định, quota requirement sẽ tăng tối đa gấp 3 lần kích thước volume source.

→ Clone một volume trong cùng một zone, nhưng các Availability Zone khác nhau yêu cầu quota bộ nhớ Swift bổ sung. Nếu không có khả năng sử dụng Swift trong trường hợp này, có thể chỉ định flag `--clone-via-snapshot`.

→ Nên tắt VM trước khi bắt đầu di chuyển VM hoặc volume.

→ Theo mặc định, cyclone ghi tất cả log yêu cầu/phản hồi của OpenStack vào một thư mục cyclone, nằm trong System Temporary Directory. Đặt flag `-d` hoặc `--debug` nếu muốn xem các log này trong console output.
