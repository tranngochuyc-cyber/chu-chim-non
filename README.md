# Circular Economy Exchange — Sàn trao đổi Đồ cũ & Tái chế

> README này được viết lại theo đúng nội dung trong ảnh yêu cầu môn học. Phạm vi triển khai được chia thành 3 phần độc lập để 3 thành viên sử dụng 3 AI khác nhau làm song song. Đây là tài liệu phân công và đặc tả, không phải xác nhận dự án đã hoàn thành hoặc đã kiểm thử.

## 1. Chủ đề và mục tiêu

**Tên phân hệ:** Sàn trao đổi Đồ cũ & Tái chế (*Circular Economy Exchange*).

Xây dựng một website hỗ trợ trao đổi các sản phẩm đã qua sử dụng, góp phần thúc đẩy kinh tế tuần hoàn bằng cách kéo dài vòng đời sản phẩm và giảm lượng rác thải.

### Tầm nhìn dài hạn

- Tích hợp Blockchain để truy xuất nguồn gốc sản phẩm.
- Sử dụng AI để định giá đồ cũ.
- Kết nối với các đơn vị vận chuyển xanh, ví dụ xe điện.

**Lưu ý:** Đây là tầm nhìn dài hạn được nêu trong đề bài, không mặc nhiên là các chức năng phải xây dựng trong phạm vi bài tập hiện tại.

## 2. Yêu cầu phải có trong đồ án

### 2.1. Công nghệ và giao diện

- **HTML5 và CSS3:** Thiết kế lưới sản phẩm (*Product Grid*) chuyên nghiệp.
- **Badges:** Dùng nhãn để thể hiện tình trạng đồ cũ. Ba nhãn được nêu trong đề:
  - `Like new`
  - `Good`
  - `Fair`

### 2.2. JavaScript

- Xử lý logic tìm kiếm sản phẩm.
- Xử lý bộ lọc sản phẩm theo **danh mục hoặc khoảng cách**.
- Viết hàm tính toán **“Lượng rác thải đã giảm thiểu”** khi người dùng thực hiện một giao dịch thành công.

### 2.3. Ba trang tối thiểu

| Trang | Nội dung bắt buộc |
|---|---|
| **Trang chủ** | Hiển thị các mặt hàng mới đăng và thống kê tổng lượng rác thải cộng đồng đã giảm thiểu. |
| **Trang Danh mục sản phẩm** | Có giao diện tìm kiếm và lọc đồ cũ theo nhiều tiêu chí. Các tiêu chí được nêu cụ thể trong yêu cầu JavaScript là danh mục hoặc khoảng cách. |
| **Trang Đăng tin** | Có form cho người dùng nhập mô tả, tải ảnh theo hình thức giả lập và chọn loại hình trao đổi: `Give`, `Sell` hoặc `Exchange`. |

## 3. Phân chia công việc cho 3 AI

Mỗi thành viên giao đúng phần việc của mình cho một AI riêng. Không để nhiều AI cùng tự xây dựng một chức năng hoặc tự ý sửa phần của thành viên khác.

### AI 1 — Trang chủ, Product Grid và Badges

**Mục tiêu:** Xây dựng phần giao diện hiển thị sản phẩm và trang chủ.

**Phạm vi công việc:**

1. Xây dựng giao diện Trang chủ.
2. Hiển thị các mặt hàng mới đăng.
3. Xây dựng Product Grid chuyên nghiệp bằng HTML5 và CSS3.
4. Thiết kế cách hiển thị thông tin sản phẩm trong lưới.
5. Hiển thị đúng ba nhãn tình trạng:
   - `Like new`
   - `Good`
   - `Fair`
6. Tạo khu vực hiển thị thống kê tổng lượng rác thải cộng đồng đã giảm thiểu. Giá trị phải lấy từ phần tính toán được tích hợp, không tự tạo số liệu.

**Không phụ trách:**

- Logic tìm kiếm và lọc của trang Danh mục sản phẩm.
- Form đăng tin.
- Logic tính lượng rác thải giảm thiểu.

**Kết quả bàn giao:** Trang chủ, Product Grid, Badges và phần hiển thị thống kê cộng đồng.

### AI 2 — Trang Danh mục sản phẩm và tìm kiếm/lọc

**Mục tiêu:** Xây dựng trang giúp người dùng tìm kiếm và lọc các sản phẩm cũ.

**Phạm vi công việc:**

1. Xây dựng giao diện Trang Danh mục sản phẩm.
2. Hiển thị các sản phẩm bằng Product Grid dùng chung do AI 1 xây dựng.
3. Dùng JavaScript xử lý tìm kiếm sản phẩm.
4. Xử lý bộ lọc theo danh mục.
5. Xử lý bộ lọc theo khoảng cách.
6. Đảm bảo có thể kết hợp các điều kiện lọc được yêu cầu và cập nhật danh sách kết quả.

**Không phụ trách:**

- Tạo một Product Grid khác trùng chức năng với AI 1.
- Xây dựng Trang chủ.
- Xây dựng form đăng tin.
- Tính lượng rác thải giảm thiểu.

**Kết quả bàn giao:** Trang Danh mục sản phẩm và logic JavaScript tìm kiếm/lọc theo đúng phạm vi yêu cầu.

### AI 3 — Trang Đăng tin và tính lượng rác thải giảm thiểu

**Mục tiêu:** Xây dựng form đăng sản phẩm và phần logic tính lượng rác thải giảm thiểu.

**Phạm vi công việc:**

1. Xây dựng giao diện Trang Đăng tin.
2. Tạo form cho người dùng nhập mô tả sản phẩm.
3. Tạo chức năng chọn ảnh theo hình thức giả lập.
4. Cho phép chọn đúng ba loại hình trao đổi:
   - `Give`
   - `Sell`
   - `Exchange`
5. Viết hàm tính toán “Lượng rác thải đã giảm thiểu”.
6. Chỉ ghi nhận lượng rác thải giảm thiểu khi có giao dịch được xác nhận thành công.
7. Cung cấp kết quả tính toán để AI 1 hiển thị tổng lượng rác thải cộng đồng đã giảm thiểu trên Trang chủ.

**Không phụ trách:**

- Xây dựng lại Trang chủ hoặc Product Grid.
- Xây dựng logic tìm kiếm/lọc của Trang Danh mục.
- Tự tạo trang thanh toán hoặc quy trình giao dịch mới ngoài yêu cầu.

**Kết quả bàn giao:** Trang Đăng tin, form đúng yêu cầu và module tính lượng rác thải giảm thiểu có thể tích hợp với Trang chủ.

## 4. Quy tắc phối hợp để 3 AI không làm sai hoặc trùng việc

### 4.1. Phân quyền theo chức năng

| Hạng mục | AI chịu trách nhiệm chính | AI còn lại được phép làm gì? |
|---|---|---|
| Trang chủ | AI 1 | Chỉ tích hợp dữ liệu thống kê do AI 3 cung cấp và chức năng liên quan đã thống nhất. |
| Product Grid | AI 1 | AI 2 sử dụng lại, không tạo bản sao. |
| Badges tình trạng sản phẩm | AI 1 | AI 2 hiển thị lại theo dữ liệu sản phẩm, không tự đổi nhãn. |
| Tìm kiếm và lọc theo danh mục/khoảng cách | AI 2 | Không viết lại Product Grid hoặc sửa form đăng tin. |
| Trang Đăng tin | AI 3 | Không sửa cấu trúc Trang chủ hoặc Trang Danh mục. |
| Tính lượng rác thải giảm thiểu | AI 3 | AI 1 chỉ nhận kết quả để hiển thị thống kê. |

### 4.2. Quy tắc dữ liệu và tích hợp

- Ba AI phải thống nhất cách biểu diễn một sản phẩm trước khi tích hợp.
- Dữ liệu sản phẩm cần đủ thông tin để hiển thị Product Grid, nhãn tình trạng và phục vụ tìm kiếm/lọc theo danh mục hoặc khoảng cách.
- Ba nhãn tình trạng phải giữ nguyên: `Like new`, `Good`, `Fair`.
- Ba loại hình trao đổi phải giữ nguyên: `Give`, `Sell`, `Exchange`.
- AI 2 phải dùng chung dữ liệu và Product Grid của AI 1, không tạo dữ liệu hoặc giao diện trùng lặp nếu không có lý do kỹ thuật được nhóm thống nhất.
- AI 3 phải cung cấp kết quả tính lượng rác thải theo một cách rõ ràng để AI 1 có thể hiển thị tổng trên Trang chủ.
- Trước khi sửa file hoặc giao diện thuộc phần của thành viên khác, AI phải báo và thống nhất với người phụ trách.
- Khi thiếu thông tin để triển khai chính xác, AI phải ghi rõ `NEED CONFIRMATION` hoặc `BLOCKED`; không tự suy diễn thành yêu cầu mới.

## 5. Những điểm đề bài chưa xác định — không được tự bịa

Ảnh yêu cầu không cung cấp đủ chi tiết cho một số quy tắc triển khai. Nhóm cần xác nhận các điểm sau trước khi chốt hành vi thực tế:

1. **Công thức lượng rác thải giảm thiểu:** Chưa có công thức, đơn vị đo, dữ liệu khối lượng hoặc hệ số quy đổi. AI 3 không được tự đặt hệ số hay tự tuyên bố một giao dịch tương ứng với một số kg rác thải. Cần xin quy tắc từ giảng viên hoặc thống nhất một giả định demo có ghi nhãn rõ ràng.
2. **Điều kiện xác định giao dịch thành công:** Ảnh yêu cầu chỉ tính khi giao dịch thành công nhưng không mô tả quy trình hoặc tín hiệu xác nhận thành công. Không được tự thêm hệ thống thanh toán hay quy trình giao dịch phức tạp; cần xác định điểm kích hoạt trước khi tích hợp.
3. **Khoảng cách:** Chưa nêu đơn vị, vị trí tham chiếu hoặc cách xác định khoảng cách. Không được tuyên bố có định vị GPS hoặc khoảng cách thực tế nếu chưa xây dựng và xác minh chức năng đó.
4. **Danh mục sản phẩm:** Ảnh không liệt kê các giá trị danh mục cụ thể. Nhóm cần thống nhất dữ liệu mẫu, không trình bày danh sách tự chọn như thể đó là danh mục bắt buộc của đề.
5. **Tình trạng sản phẩm:** Ảnh chỉ nêu ba nhãn `Like new`, `Good`, `Fair`, chưa đưa ra tiêu chuẩn chi tiết để phân loại từng nhãn.
6. **Ảnh đăng sản phẩm:** Yêu cầu ghi rõ tải ảnh giả lập. Không được tuyên bố ảnh đã được tải lên máy chủ hoặc lưu trữ trực tuyến.
7. **Dữ liệu và lưu trữ:** Ảnh không quy định backend, cơ sở dữ liệu, tài khoản người dùng hoặc cách lưu tin đăng. Không tự thêm các hệ thống này vào phạm vi bắt buộc.

## 6. Prompt giao việc cho từng AI

Mỗi thành viên chỉ gửi prompt tương ứng với phần được phân công. AI phải đọc toàn bộ README trước khi thực hiện.

### Prompt AI 1 — Home + Product Grid + Badges

```text
Bạn phụ trách AI 1 của dự án Circular Economy Exchange.

Đọc README.md và chỉ triển khai các hạng mục được giao cho AI 1:
1. Trang chủ hiển thị các mặt hàng mới đăng.
2. Product Grid chuyên nghiệp bằng HTML5 và CSS3.
3. Badges tình trạng sản phẩm với đúng ba nhãn: Like new, Good, Fair.
4. Khu vực hiển thị tổng lượng rác thải cộng đồng đã giảm thiểu.

Không làm phần tìm kiếm/lọc của Trang Danh mục.
Không làm form Đăng tin.
Không tự viết công thức tính lượng rác thải.

Phải dùng dữ liệu sản phẩm và quy ước tích hợp thống nhất với AI 2 và AI 3.
Giá trị thống kê trên Trang chủ phải lấy từ module tính toán được tích hợp.
Nếu module chưa có dữ liệu hợp lệ, hiển thị trạng thái chưa có dữ liệu; tuyệt đối không tạo số liệu giả.

Không tự thêm chức năng ngoài README.
Không sửa phần việc thuộc AI 2 hoặc AI 3.
Nếu thiếu thông tin, ghi rõ NEED CONFIRMATION thay vì tự suy diễn.

Bàn giao:
- Các file thuộc Trang chủ, Product Grid và Badges.
- Danh sách file đã thay đổi.
- Cách tích hợp với AI 2 và AI 3.
- Kết quả kiểm tra thực tế; phân biệt PASS, FAIL, BLOCKED và NOT RUN.
```

### Prompt AI 2 — Category + Search + Filter

```text
Bạn phụ trách AI 2 của dự án Circular Economy Exchange.

Đọc README.md và chỉ triển khai các hạng mục được giao cho AI 2:
1. Trang Danh mục sản phẩm.
2. Hiển thị danh sách sản phẩm bằng Product Grid dùng chung của AI 1.
3. JavaScript tìm kiếm sản phẩm.
4. Bộ lọc theo danh mục.
5. Bộ lọc theo khoảng cách.

Không tạo Product Grid thứ hai.
Không tự sửa hoặc thay thế giao diện chung của AI 1.
Không làm Trang chủ.
Không làm form Đăng tin.
Không làm chức năng tính lượng rác thải giảm thiểu.

Phải sử dụng chung cấu trúc dữ liệu sản phẩm với AI 1.
Không tự thêm bộ lọc giá, đánh giá, độ phổ biến hoặc các tiêu chí không được yêu cầu.
Đơn vị và cách xác định khoảng cách chưa được đề bài quy định; không tự tuyên bố có định vị thực tế. Nếu thiếu quy tắc, ghi NEED CONFIRMATION.

Không tự thêm chức năng ngoài README.
Không sửa phần việc thuộc AI 1 hoặc AI 3.

Bàn giao:
- Trang Danh mục sản phẩm.
- Logic JavaScript tìm kiếm và lọc.
- Danh sách file đã thay đổi.
- Cách sử dụng Product Grid và dữ liệu chung.
- Kết quả kiểm tra thực tế; phân biệt PASS, FAIL, BLOCKED và NOT RUN.
```

### Prompt AI 3 — Listing + Waste Reduction

```text
Bạn phụ trách AI 3 của dự án Circular Economy Exchange.

Đọc README.md và chỉ triển khai các hạng mục được giao cho AI 3:
1. Trang Đăng tin.
2. Form nhập mô tả sản phẩm.
3. Chức năng chọn ảnh giả lập.
4. Lựa chọn loại hình trao đổi với đúng ba giá trị:
   Give, Sell, Exchange.
5. Module tính “Lượng rác thải đã giảm thiểu” khi có giao dịch được xác nhận thành công.
6. Cung cấp tổng kết quả tính toán để AI 1 hiển thị trên Trang chủ.

Không làm Trang chủ.
Không làm Product Grid.
Không làm logic tìm kiếm/lọc.
Không tự tạo trang thanh toán hoặc hệ thống giao dịch ngoài phạm vi.

CỰC KỲ QUAN TRỌNG:
Đề bài không cung cấp công thức, đơn vị, khối lượng hoặc hệ số quy đổi lượng rác thải.
Không được tự bịa công thức hoặc số liệu.
Hãy tách riêng hàm tính toán, ghi rõ dữ liệu đầu vào cần có và đánh dấu phần công thức là NEED CONFIRMATION cho đến khi nhóm/giảng viên xác nhận.
Chỉ ghi nhận khi giao dịch có tín hiệu xác nhận thành công; không tính khi chỉ mới đăng tin.
Ảnh chỉ yêu cầu tải ảnh giả lập, không được tuyên bố đã upload lên máy chủ.

Không tự thêm chức năng ngoài README.
Không sửa phần việc thuộc AI 1 hoặc AI 2.

Bàn giao:
- Trang Đăng tin và form.
- Module tính lượng rác thải giảm thiểu.
- Quy tắc kích hoạt tính toán và dữ liệu đầu vào.
- Giao diện tích hợp kết quả với AI 1.
- Các điểm còn NEED CONFIRMATION.
- Kết quả kiểm tra thực tế; phân biệt PASS, FAIL, BLOCKED và NOT RUN.
```

## 7. Checklist nghiệm thu theo đúng yêu cầu

### AI 1
- [ ] Có Trang chủ.
- [ ] Hiển thị các mặt hàng mới đăng.
- [ ] Có Product Grid được thiết kế bằng HTML5 và CSS3.
- [ ] Có badges `Like new`, `Good`, `Fair`.
- [ ] Có khu vực hiển thị tổng lượng rác thải cộng đồng đã giảm thiểu.
- [ ] Không hiển thị số liệu rác thải tự tạo.

### AI 2
- [ ] Có Trang Danh mục sản phẩm.
- [ ] Có chức năng tìm kiếm.
- [ ] Có bộ lọc theo danh mục.
- [ ] Có bộ lọc theo khoảng cách.
- [ ] Dùng chung dữ liệu và Product Grid, không tạo bản sao không cần thiết.

### AI 3
- [ ] Có Trang Đăng tin.
- [ ] Form cho phép nhập mô tả.
- [ ] Có chức năng chọn ảnh giả lập.
- [ ] Có lựa chọn `Give`, `Sell`, `Exchange`.
- [ ] Có hàm tính lượng rác thải giảm thiểu.
- [ ] Chỉ ghi nhận giao dịch thành công.
- [ ] Công thức và đơn vị được xác nhận, không dùng số liệu tự bịa.
- [ ] Có thể cung cấp tổng kết quả cho Trang chủ.

### Toàn nhóm
- [ ] Có đủ ba trang tối thiểu theo đề.
- [ ] Ba phần dùng chung quy ước dữ liệu và tích hợp.
- [ ] Không có hai AI cùng viết một chức năng.
- [ ] Không tự đưa tầm nhìn dài hạn thành chức năng bắt buộc.
- [ ] Mọi nội dung chưa được đề bài xác định đều được đánh dấu để xác nhận.
- [ ] Chỉ đánh dấu PASS cho nội dung đã thực sự kiểm tra.

---

**Nguyên tắc cuối cùng:** Bám sát yêu cầu trong ảnh. Ưu tiên làm đúng ba trang, Product Grid/Badges, tìm kiếm/lọc và tính lượng rác thải giảm thiểu. Không tự mở rộng dự án sang các chức năng không được giao.
