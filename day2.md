# Ngày 2
1. **Shell script**
    1. **Variables**
        - Tham khảo:
        [Variables 1](https://www.shellscript.sh/variables1.html) [Variables 2]()       [Variables 3]()
        <br>
        - **Lưu ý 1: Scope of variables:**
            - Khi thực thi một file script, shell sẽ tạo ra một shell con để thực thi chương trình đó. Muốn shell con có thể kế thừa các giá trị của biến trong shell hiện tại, chúng ta dùng từ khoá <code>export</code>.
            
            - Shell con thực thi file script nếu có thay đổi đến biến môi trường của shell hiện tại sẽ chỉ có tác dụng trên môi trường của shell con. Nếu muốn thay đổi được lưu lại ở cả shell hiện tại, chúng ta sử dụng lệnh <code>.</code> (source). ví dụ: <code>. ./command.sh</code>. Lệnh source sẽ không tạo ra shell con để thực thi file chỉ định, chính vì thế chúng ta cũng không cần <code>export</code>
            <br>
        - **Lưu ý 2: Biến dòng lệnh (Command-line arguments variables)**
            - $1 ... $9: các tham số theo thứ tự khi nhập ở dòng lệnh
            - $0: tên của chương trình
            - $@: danh sách tất cả các tham số được truyền vào chương trình
            - $#: số lượng tham số được truyền vào chương trình
            - $?: exit value (== 0 nếu chạy tốt, != 0 nếu chạy lỗi)
            - $$: PID của shell hiện tại
            <br>
        - **Lưu ý 3: IFS**
            - IFS (Internal Field Separator) mặc định là SPACE, TAB, NEWLINE.
            <br>
    2. **Wildcards:** dấu <code>*</code> - đại diện cho tất cả giá trị thích hợp
    <br>
    3. **Escape characters**
    <br>
    4. **Loops**
        - **for loop**

                for item in list
                do
                    commands
                done

            Trong đó:
            - <code>item</code> là tên biến được sử dụng để lưu trữ từng phần tử trong danh sách.
            - <code>list</code> là danh sách các phần tử mà vòng lặp sẽ duyệt qua 
            - <code>commands</code> là các lệnh muốn thực hiện   
        
        - **while loop**

                while [ condition ]
                do
                    commands
                done
            
            Trong đó:
            - <code>[condition]</code> là điều kiện kiểm tra 
            - <code>commands</code> là các lệnh muốn thực hiện
            - lưu ý khoảng trắng giữa condition và []
        <br>
    Tham khảo: [Loops](https://www.shellscript.sh/loops.html)
    <br>
    5. **Test and case**
        - **Test**

                if [ condition ]
                then 
                    # if-code
                elif
                    # elif-code
                else
                    #else-code
                fi

        - **Case**

                case expression in
                    pattern1)
                        commands1 ;;
                    pattern2)
                        commands2 ;;
                    pattern3)
                        commands3 ;;
                    *)
                        default_commands ;;
                esac
        <br>
    6. **External Programs**

        1. <code>grep [option...] pattern [file...]</code> 
            - grep in ra cácc dòng trong file chỉ định mà match với pattern
            - Một số tuỳ chọn phổ biến:
            1. <code> -e PATTERNS, --regexp=PATTERNS</code>: chỉ định tìm kiếm theo pattern cụ thể, có thể sử dụng tuỳ chọn này nhiều lần.
            ví dụ: <code>grep -e systemd -e root /etc/passwd</code>
            2. <code> -f FILE, --file=FILE</code>: chỉ định tìm kiếm theo từng pattern trong file cụ thể (1 dòng trong file là một pattern)
            3. <code> -i --ignore-case</code>: không phân biệt chữ hoa, chữ thường
            4. <code> -v, --invert-match</code>: tìm kiếm các line không có pattern chỉ định
            <br>
        2. <code>cut [option...] file </code>: in ra phần được chỉ định trong mỗi dòng của file
            - <code> -d, --delimiter=DELIM</code>: sử dụng dấu phân cách chỉ định để phân tách file thay cho dấu phân cách mặc định (TAB)
            - <code> -f, --fields=LIST</code>: chỉ chọn các field được chỉ định, đồng thời in ra các dòng không có dấu phân cách (delimiter)
            - <code> -s, --only-delimitted</code>: không in ra các dòng mà không có delimiter
            <br>
    
    7. **Function**
    <br>
2. **gawk**
    


        

            
    
                
