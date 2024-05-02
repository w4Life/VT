# Ngày 4: Docker (tiếp)

1. **Dockerfile**
    Dockerfile là file văn bản có chứa các hướng dẫn để Docker xây dựng Docker image (bao gồm đóng gói sourc code, cài đặt các công cụ để chạy dự án)
    <br>
2. **Dockerfile commands**
    1. **FROM**
        - <code>FROM</code> có nhiệm vụ xác định base image mà chúng ta sẽ sử dụng cho dự án của chúng ta
        - Ví dụ: chúng ta muốn dựng một dự án sử dụng nodejs, chúng ta sẽ cần image của nodejs: <code> FROM node:20 </code> (node version 20)
    2. **WORKDIR**
        - <code> WORKDIR {path} </code> để chỉ định thư mục làm việc của dự án. ví dụ: <code>WORKDIR /app </code>
        <br>
    3. **COPY**
        - <code>COPY {src} {dest} </code> dùng để sao chép các tệp và thư mục từ máy chủ lưu trữ vào Docker image. Trong đó: {src} là đường dẫn tới tệp hoặc thư mục trên máy chủ lưu trữ, {dest} là đường dẫn tới đích trong Docker image mà ta đang xây dựng.
        - Ví dụ <code>COPY . . </code>: <code>.</code> đầu tiên chỉ thư mục hiện tại của Dockerfile, <code>.</code> thứ hai chỉ thư mục làm việc được chỉ định trước đó bằng <code>WORKDIR</code>
        <br>
    4. **RUN**
        - <code>RUN commands</code>, trong đó commands là câu lệnh ta muốn thực thi trong quá trình build image, tức chỉ **chạy 1 lần duy nhất**. ví dụ <code>RUN pwd</code>
        <br>
    5. **ENV**
        - <code>ENV {key} {value}</code> để định nghĩa các biến môi trường cho Docker image. Các biến môi trường có thể được sử dụng trong quá trình xây dựng image.
        - Ví dụ

                ENV APP /usr/src/app
                WORKDIR $APP
                COPY . $APP

            <br>
    6. **EXPOSE**
        - <code>EXPOSE {port}</code> được sử dụng để chỉ định port mà container sẽ lắng nghe các kết nối từ bên ngoài (lưu ý: EXPOSE không mở port của container, nó chỉ hướng dẫn người dùng port nào của container được chỉ định để lắng nghe)
        <br>
    7. **CMD và ENTRYPOINT**
        - Chỉ định các lệnh sẽ chạy khi container được khởi động. <code>cmd</code> có thể bị ghi đè còn <code>entrypoint</code> thì không.
        - có thể buổi diễn dưới dạng command hoặc array
        <br>
3. **Tư duy viết Dockerfile tối ưu**
    - **non root user**: Không sử dụng user root để triển khai dự án
    - **chọn base image phù hợp**
    - **multiple stage**