# Clean code in Unity
## Clean code là gì? Tại sao cần clean code?

- Clean code (mã sạch) là một khái niệm trong lập trình phần mềm, đề cập đến việc viết mã nguồn sao cho dễ đọc, dễ hiểu và
dễ bảo trì.
- Mục tiêu của clean code là giúp các lập trình viên khác (hoặc chính bạn trong tương lai) có thể nhanh chóng
hiểu được ý định của mã nguồn, giảm thiểu lỗi và tăng hiệu suất làm việc.

## Clean code nên bắt đầu từ đâu?

1. **Đặt tên biến và hàm rõ ràng**:
    - Một tên biến/hàm được xem là tốt khi các lập trình viên khác nhau đọc đều có thể hiểu được biến/hàm đó
      dùng để làm gì.
    - Tên biến và tên hàm phải là tên có nghĩa
    - Chữ cái đầu tiên của biến sẽ là chữ thường, các chữ cái đầu tiên của các từ tiếp theo sẽ viết hoa (ví dụ:
      `string studentName = "VirtueSky";`, `int calculateTotal = 0`).
    - Không sử dụng tên có ký tự đầu tiên là số (ví dụ: `int d = 365;`)
    - Đối với tên hàm cũng tương tự tuy nhiên chữ cái bắt đầu của tên hàm sẽ là chữ in hoa, (ví dụ: `GetDayInYear(){}`)
    - Không viết tắt trong tên biến hoặc tên hàm.
    - Sử dụng tên biến nhất quán trong suốt project
      (ví dụ: `const int DAYS_IN_WEEK = 7;` or `const int daysInWeek = 7;`) trong 2 kiểu tên biến const ở ví dụ, nếu đã
      follow theo kiểu nào sẽ làm tương tự xuyên suốt project.
2. **If-Else và Switch-case**
