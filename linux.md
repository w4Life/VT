# linux
1. **Cron**
    1. **Định nghĩa**
        Là một chương trinh lập lịch dựa trên thời gian. Sử dụng lệnh <code>cron</code> để lập lịch, tạo các công việc tự động (cron jobs).
        <br>
    
    2. **Hiểu cách Cron hoạt động**
        Cron jobs được ghi lại và quản lý trong một file <code>crontab</code>. Mỗi một user sẽ có file crontab riêng, được lưu trong thư mục <code>/var/spool/cron/crontabs</code>. Mỗi user sẽ chỉnh sửa lịch làm việc trong file crontab riêng theo cấu trúc sau:

        <code>minute</code> <code>hour</code> <code>day_of_month</code> <code>month</code> <code>day_of_week</code> <code>command_to_run</code>

        | Field | Allowed Values |
        | --- | --- |
        | minute | 0 - 59 |
        | hour | 0 - 23 |
        | day_of_month | 1 - 31 |
        | month | 1 - 12 hoặc JAN - DEC |
        | day of the week | 0 - 6 hoặc SUN - SAT|

        ví dụ : <code>30 17 * * curl https://google.com</code>

        Một số kí tự đặc biệt:
        1. <code>*</code>: Trong biểu thức cron, dấu * đại diện cho tất cả các giá trị
        2. <code>,</code>: tạo một danh sách các giá trị trong mỗi trường. Ví dụ: <code>20,30 * * * curl https://google.com</code> sẽ thực hiện lệnh curl tới google mỗi phút 20 và 30 của tất cả các giờ trong ngày trong tháng
        3. <code>-</code>: dấu - đại diện cho một khoảng dữ liệu
        4. <code>/</code>: dấu / sử dụng cùng dấu * để thể hiện các giá trị cách đều nhau. Ví dụ: <code>0 */3 * * ...</code> sẽ thực hiện lệnh vào mỗi 3 phút.
        <br>
    
    3. **Quản lý crontabs**
        <code>man crontab</code> để biết thêm chi tiết
        <br>

    **Tham khảo**
    [Cron](https://www.digitalocean.com/community/tutorials/how-to-use-cron-to-automate-tasks-ubuntu-1804)
    <br>

2. **Storage**
    1. **Block Storage**
        Là kiểu lưu trữ dữ liệu sử dụng các khối (~ a piece of hardware that can be used to store data), Mỗi block được xem là độc lập, và có thể truy cập đọc, ghi trên mỗi khối. Các khối này được quản lý bở hệ thống tệp tin (filesystem) để tạo thành các tệp và thư mục.
        <br>
    2. **Phân vùng ổ cứng (Disk Partitions)**
        Disk Partitions là cách chia thiết bị lưu trức ra thành các đơn vị nhỏ hơn có thể sử dụng được. Một phân vùng là một phần của thiết bị lưu trữ và có thể xem như 1 thiết bị lưu trữ.
        <br>
        Khi phân vùng cần nắm rõ format sẽ sử dụng. Hiện nay format phổ biến khi phân vùng là **GPT(GUID Partition Table)**. 
        <br>
    3. **Formatting and Filesystem**
        **Formatting** là quá trình tạo một hệ thống tệp tin (filesystem) lên ổ đĩa và chuẩn bị việc vận hành file.
        **Filesystem** là hệ thống cấu trúc dữ liệu và kiểm soát việc ghi và lấy dữ liệu ở ổ đĩa.
        <br>
        Một số kiểu filesystem:
        - **Ext4**: filesystem phổ biến trong hầu hết các Linux-distro. Ext4 có cơ chế journal (cơ chế đảm bảo tính toàn vẹn và nhất quán cho dữ liệu)
        - **XFS**: hiệu suất cao, làm việc tốt với các tập tin có dung lượng lớn. nhưng có rủi ro về việc hỏng hóc dữ liệu
        - **NTFS**: filesystem của Windows.
        <br>
    4. **Cách Linux quản lý thiết bị lưu trữ**
        - **file trong /dev** 
            Các file ánh xạ với các ổ cứng sẽ bắt đầu với tiền tố <code>sd</code> hoặc <code>hd</code>. 
            Các phân vùng sẽ có tên file là <code>/dev/sda1</code> hoặc <code>/dev/hda1</code>, ...

        - **/dev/disk/**
            chứa các thư mục con tương ứng với cấc cách quản lý phân vùng khác nhau. Mỗi phân vùng được quản lý trong đây có thể link về <code>/dev/[s,h]d...</code>
            - <code>by-label</code>
            - <code>by-uuid</code>
            - <code>by-partlabel</code> hoặc <code>by-partuuid</code>
            - <code>by-id</code>
            ...
            <br>

    5. **Mounting Block Devices**
        **Mounting**: là quá trình đưa một hệ thống tập tin vào cây thư mục của hệ thống, làm cho dữ liệu trong hệ thống tập tin đó có thể được sử dụng, truy cập thông qua cây thư mục.
        Chúng ta có thể sử dụng <code>/etc/fstab</code> để thực hiện mounting. Chi tiết tự tìm hiểu.
        <br>

    **Tham khảo:** [Introduction to Storage in Linux](https://www.digitalocean.com/community/tutorials/an-introduction-to-storage-terminology-and-concepts-in-linux#making-mounts-permanent-with-etc-fstab)
    <br>
3. **Network Command**
    - [Networking key concepts](https://ubuntu.com/server/docs/networking-key-concepts)
    - [Configuring networks](https://ubuntu.com/server/docs/configuring-networks)

4. **Search, manipulate, ...**
    1. **Search**: <code>find [path] [options] [expression]</code>
        - <code> -name {name} </code>: tìm theo tên đối tượng 
        - <code> -size {size} </code>: tìm theo kích cỡ. c - bytes, K - kilobytes, M - megabytes, G - gigabytes
        - <code> -perm {permission} </code>: tìm theo phân quyền của đối tượng. ví dụ <code>sudo find /var/log/ -perm -g=w ! -perm /o=rw > /home/bob/data.txt</code>
            - -perm -g=w: ít nhất có quyền w của group
            - ! -perm /o=rw: others không có quyền r w
    2. **sed, cut, sort, uniq, grep**
    3. **regex expression**

5. **Archive, Compress, Backup**
    1. **Archive, Compress** : <code>tar</code> kết hợp cùng <code>gzip, bzip2, xzip</code>
    2. **Backup**: chiến lược cơ bản - backup từ hệ thống này sang hệ thống khác
        - rsync - remote synchronization
        ![rsync](./image/remote%20synchronization.png)
        - <code> rsync [options] {source} {dest} </code>
        - ví dụ: <code>rsync -a . kmhai@1.1.1.1:/backups</code> 

    