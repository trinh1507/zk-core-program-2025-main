ZKAuth: Zero-Knowledge Password Authentication

📋 Mục lục

Giới thiệu

Thành viên nhóm

Tóm tắt kỹ thuật

Demo & Video hướng dẫn

Cấu trúc dự án

Hướng dẫn cài đặt & sử dụng

Khuyến nghị bảo mật

License

Giới thiệu

ZKAuth là một hệ thống xác thực mật khẩu an toàn bằng Zero-Knowledge Proof (ZKP). Người dùng có thể chứng minh họ biết mật khẩu hợp lệ mà không tiết lộ mật khẩu đó cho server.

Công nghệ chính:

Circom: định nghĩa và compile circuit cho ZKP.

SnarkJS + PLONK: thực hiện trusted setup, sinh proof và verify proof.

Thành viên nhóm

Leader: Hà Duy Nhất

Members:

Phạm Đăng Trình

Trương Văn Thịnh

Nguyễn Thanh Truyền

Nguyễn Huỳnh Quang

Nguyễn Đại Phát

Tóm tắt kỹ thuật

Signup

Nhúng mật khẩu (chuyển thành số) vào circuit Circom.

Biên dịch circuit → R1CS + WASM + SYM.

Thiết lập PLONK trusted setup → tạo circuit_final.zkey.

Xuất verification key ra verification_key.json.

Login

Người dùng nhập mật khẩu.

Dùng circuit.wasm + circuit_final.zkey → sinh proof (snarkjs.plonk.fullProve).

Đọc publicSignals[0] (1 = đúng, 0 = sai).

Server verify proof bằng verification_key.json.

Demo & Video hướng dẫn

Video demo tính năng Signup & Login: ./demo.mp4

Link xem trực tuyến: https://www.youtube.com/watch?v=6KJdHLKjJ1U

Cấu trúc dự án

zkpasswords-main/
├─ circom/                 # Mã nguồn Circom
├─ public/                 # Front-end (HTML, JS)
│   ├─ signup.html
│   ├─ signup.js
│   ├─ login.html
│   ├─ login.js
│   ├─ home.html
│   └─ change.html
├─ zkauth/                 # Module ZKAuth gốc
│   ├─ setup.sh            # Script tự động build ZKP
│   ├─ pot14_final.ptau    # Tham số chung PLONK
│   └─ circuit_final.zkey  # Proving + verification key mẫu
├─ zkauthaccounts/         # Thư mục lưu artifact cho từng user
├─ server.js               # Express API
├─ package.json            # Dependencies & scripts
└─ README.md               # Tài liệu này

Hướng dẫn cài đặt & sử dụng

Cài đặt:

npm install

Chạy server:

node server.js

Mở trình duyệt tại http://localhost:3000/signup để đăng ký, sau đó http://localhost:3000/login để đăng nhập.

Khuyến nghị bảo mật

Sử dụng HTTPS cho môi trường production.

Bảo vệ thư mục zkauthaccounts/ khỏi truy cập trái phép.

Không lưu trữ plaintext hoặc hash mật khẩu.