# Study Space Finder — Hướng dẫn triển khai đồ án cuối kỳ nhóm 3 bằng Antigravity và GitHub Pages

> **Tài liệu dành cho nhóm 3 sinh viên làm việc trên 3 máy trường.** Phương án giữ nguyên phạm vi: A làm kiến trúc, giao diện chính, tìm kiếm và tích hợp; B làm dữ liệu và thẻ địa điểm; C làm yêu thích, kiểm thử và tài liệu. Cả ba sử dụng Antigravity, một repository GitHub và GitHub Pages.  
> **Quan trọng:** Đây là tài liệu hướng dẫn, không phải báo cáo xác nhận dự án đã được tạo, đã kiểm thử hay đã deploy.

## Mục lục

1. [Phương án làm việc của nhóm](#1-phương-án-làm-việc-của-nhóm)
2. [Chuẩn bị GitHub và Antigravity trên máy trường](#2-chuẩn-bị-github-và-antigravity-trên-máy-trường)
3. [Mở dự án trong Antigravity](#3-mở-dự-án-trong-antigravity)
4. [Khóa cấu trúc và hợp đồng kỹ thuật](#4-khóa-cấu-trúc-và-hợp-đồng-kỹ-thuật)
5. [Ba prompt cố định cho ba thành viên](#5-ba-prompt-cố-định-cho-ba-thành-viên)
6. [Hai cách đưa code lên GitHub: push hoặc ZIP](#6-hai-cách-đưa-code-lên-github-push-hoặc-zip)
7. [Ghép code và cho Antigravity kiểm tra web](#7-ghép-code-và-cho-antigravity-kiểm-tra-web)
8. [Prompt kiểm tra tích hợp, tự đề xuất người sửa](#8-prompt-kiểm-tra-tích-hợp-tự-đề-xuất-người-sửa)
9. [Checklist và lưu ý](#9-checklist-và-lưu-ý)
10. [Giải đáp: Có cần kết nối GitHub để prompt chính xác nhất không?](#10-giải-đáp-có-cần-kết-nối-github-để-prompt-chính-xác-nhất-không)
11. [Nguồn tham khảo chính thức](#11-nguồn-tham-khảo-chính-thức)

---

## 1. Phương án làm việc của nhóm

```
                     GitHub repository: study-space-finder
                       main + docs/CONTRACT.md
                                |
                +---------------+---------------+
                |               |               |
          Thành viên A     Thành viên B     Thành viên C
          feature/core    feature/space-cards  feature/favorites-qa
          Core + UI/UX     Dữ liệu + Card   Yêu thích + QA
                |               |               |
                +--------- Pull Requests --------+
                                |
                            Merge main
                                |
                  Antigravity A kiểm tra tổng thể
                                |
                          GitHub Pages
```

### Phân công cố định

| Người | Nhiệm vụ | Phần quan trọng khi bảo vệ |
|---|---|---|
| **A — Trưởng nhóm** | Giao diện chính, tìm kiếm, lọc, sắp xếp, kết nối module, triển khai | Giải thích kiến trúc và luồng hoạt động |
| **B — Thành viên 2** | Dữ liệu JSON, card, cửa sổ xem chi tiết | Giải thích dữ liệu, DOM và event |
| **C — Thành viên 3** | Yêu thích, giao diện yêu thích, kiểm thử, tài liệu | Giải thích localStorage và kiểm thử |

Không đổi phân công khi phát sinh lỗi. Antigravity sẽ phân tích và **đề xuất** giao lỗi cho đúng người phụ trách; quyết định triển khai thuộc nhóm.

### Mục tiêu sản phẩm

Website tĩnh tìm địa điểm học tập dành cho sinh viên, có thanh tìm kiếm, bộ lọc theo khu vực/loại/giá/độ ồn/tiện ích, sắp xếp, thẻ địa điểm, chi tiết địa điểm và lưu yêu thích. Tối ưu sử dụng trên desktop và điện thoại; dữ liệu minh họa phải ghi rõ là **DEMO**. Không tự tạo chức năng đặt chỗ, backend, dữ liệu chỗ trống theo thời gian thực hay đánh giá người dùng giả.

Công nghệ: **HTML5 + CSS3 + JavaScript ES Modules + JSON + localStorage + Git/GitHub + GitHub Pages**, không React/Vue hoặc quá trình build.

---

## 2. Chuẩn bị GitHub và Antigravity trên máy trường

1. Trên trình duyệt máy trường, mở <https://github.com/new>.
2. Tạo repository tên **`study-space-finder`**, nên chọn **Public** để dùng GitHub Pages với tài khoản GitHub Free.
3. Đánh dấu **Add a README file** và tạo repository.
4. Vào **Settings → Collaborators → Add people** và mời hai thành viên còn lại bằng tài khoản GitHub thật. Hai bạn cần chấp nhận lời mời.
5. Lấy URL từ **Code → HTTPS**, có dạng:

   `https://github.com/USERNAME/study-space-finder.git`

6. Người A tạo **bản nền + `docs/CONTRACT.md` trên main** và push trước. B và C **chỉ tạo branch từ main sau khi nhận bản nền**.

**Lưu ý máy trường:** Dữ liệu trên ổ máy có thể bị xóa sau buổi học, nên các thay đổi quan trọng phải được commit/push lên GitHub hoặc có một bản sao ZIP đáng tin cậy. Không lưu mật khẩu hay access token vào file nguồn. Đăng xuất GitHub và xóa thông tin đăng nhập còn lưu khi rời máy dùng chung.

---

## 3. Mở dự án trong Antigravity

### Cách chuẩn: Clone repository vào workspace

1. Mở **Antigravity** trên máy trường.
2. Nếu giao diện có **Clone Repository**, chọn mục đó, dán URL HTTPS của repo và chọn thư mục có quyền ghi. Hoặc mở **Terminal → New Terminal** và chạy:

   ```powershell
   git clone https://github.com/USERNAME/study-space-finder.git
   cd study-space-finder
   ```

3. Chọn **Open Folder** hoặc **New Project → Add Folder → Create** để thêm đúng thư mục đã clone vào workspace.
4. Trong Antigravity Agent, chọn chế độ **Local** nếu muốn làm trực tiếp trong thư mục đã mở. Nếu dùng chế độ **Worktree**, phải nhận diện đúng worktree và branch trước khi commit/push.
5. Dán prompt dành cho người đó vào ô chat Agent. Khi Agent yêu cầu chạy lệnh, cần đọc lệnh trước khi phê duyệt.

**Antigravity có thể thao tác với các file trong workspace đã mở**, nhưng không tự có source của người khác nếu chưa clone/pull phiên bản mới nhất. Việc đăng nhập Antigravity bằng tài khoản Google **khác** với xác thực GitHub để push code.

---

## 4. Khóa cấu trúc và hợp đồng kỹ thuật

Cấu trúc chung duy nhất:

```text
study-space-finder/
├── index.html
├── .nojekyll
├── README.md
│
├── assets/
│   ├── css/
│   │   ├── base.css
│   │   ├── space-cards.css
│   │   └── favorites.css
│   └── js/
│       ├── app.js
│       ├── search.js
│       ├── components/
│       │   └── space-cards.js
│       └── features/
│           └── favorites.js
│
├── data/
│   └── spaces.json
│
└── docs/
    ├── CONTRACT.md
    ├── ARCHITECTURE.md
    ├── UX-RESEARCH.md
    ├── WORKLOG-A.md
    ├── WORKLOG-B.md
    ├── WORKLOG-C.md
    ├── TEST-REPORT.md
    └── DEFENSE-NOTES.md
```

### Mẫu một object trong `data/spaces.json`

```json
{
  "id": "space-01",
  "name": "Study Corner Demo",
  "district": "Khu vực A",
  "address": "Địa chỉ minh họa",
  "type": "cafe",
  "pricePerHour": 20000,
  "noiseLevel": "quiet",
  "amenities": ["wifi", "outlet", "ac"],
  "hours": "07:00 - 22:00",
  "description": "Không gian học tập yên tĩnh."
}
```

`spaces.json` phải chứa **một mảng JSON** gồm nhiều object như trên. `type` chỉ nhận `cafe | library | coworking`; `noiseLevel` chỉ nhận `quiet | moderate | lively`; `amenities` chỉ nhận các giá trị trong `wifi | outlet | ac | parking`. `pricePerHour` là số nguyên không âm, đơn vị VND, `0` nghĩa là miễn phí. `id` là chuỗi duy nhất.

### Public API bất biến

**B** cung cấp file `assets/js/components/space-cards.js`:
- `createSpaceCard(space, { isFavorite, onViewDetail, onToggleFavorite })` → `HTMLElement`.
- `openSpaceDetails(space, { isFavorite, onToggleFavorite })` → mở dialog chi tiết.
- `onViewDetail(id)` nhận ID địa điểm.
- `onToggleFavorite(id)` trả về `boolean` là trạng thái yêu thích mới.

**C** cung cấp file `assets/js/features/favorites.js`:
- `getFavoriteIds()` → `string[]`.
- `toggleFavorite(id)` → `string[]` mới.
- `renderFavoritesToolbar(container, { count, showOnlyFavorites, onToggle })` → render/cập nhật toolbar.
- Storage key: `study-space-finder:favorites:v1`.

**A** chịu trách nhiệm gọi và kết nối các API của B/C. Không đổi field, chữ ký hàm hoặc tên file khi chưa thống nhất. Mỗi người chỉ được chỉnh file của mình; nếu phát hiện thiếu sót trong contract, báo nhóm thay vì tự thay đổi.

---

## 5. Ba prompt cố định cho ba thành viên

### Prompt A — Trưởng nhóm: Core, UI/UX, contract và tích hợp

> **Dán nguyên prompt này vào Antigravity Agent của người A.**

```text
# ANTIGRAVITY — STUDY SPACE FINDER — MEMBER A

VAI TRÒ: Technical Lead, Frontend Engineer và UI/UX Designer.

Bạn đang hỗ trợ trưởng nhóm phát triển đồ án cuối kỳ Study Space Finder. Nhóm gồm 3 sinh viên sử dụng Google Antigravity trên 3 máy trường khác nhau.

MỤC TIÊU CHUNG:
Website tìm kiếm không gian học tập cho sinh viên, chạy bằng GitHub Pages, thiết kế hiện đại, dễ sử dụng, có tìm kiếm, lọc, sắp xếp, chi tiết địa điểm và lưu yêu thích.

Không xây dựng website đặt chỗ, mạng xã hội, hệ thống quản trị hoặc ứng dụng có backend.

CÔNG NGHỆ CỐ ĐỊNH:
HTML5, CSS3, JavaScript ES Modules, JSON, localStorage, Git/GitHub. Không React, Vue, npm dependencies hoặc build process.

## 1. Môi trường làm việc

- Chỉ sử dụng workspace của Antigravity trên máy trường.
- Không giả định tồn tại file trên máy cá nhân.
- Mọi thay đổi quan trọng phải được lưu trên GitHub.
- Không truy cập hoặc chỉnh sửa file ngoài workspace.
- Trước mọi thao tác Git, kiểm tra repository, remote, branch và trạng thái.
- Không force push, xóa lịch sử hoặc ghi đè file người khác.
- Không lưu thông tin đăng nhập, token hay mật khẩu vào source.

Nếu repo chưa được clone:
- Hướng dẫn người dùng lấy URL GitHub thật.
- Clone repo vào thư mục được máy trường cho phép.
- Mở toàn bộ repo làm workspace.

## 2. Giai đoạn đầu — bắt buộc thực hiện trước khi nhóm làm song song

Tạo và commit bản nền trên main, gồm:
- docs/CONTRACT.md
- docs/ARCHITECTURE.md
- docs/UX-RESEARCH.md
- docs/WORKLOG-A.md
- index.html ở trạng thái skeleton hợp lệ
- .nojekyll
- assets/css/base.css với design tokens ban đầu

Trong CONTRACT.md, phải viết chính xác quy định dữ liệu, public API, phạm vi file của ba thành viên và cách kết nối module được mô tả dưới đây.

Push base commit lên GitHub. Báo người dùng tên commit và xác nhận hai thành viên có thể tạo branch từ main.

Không triển khai thay phần B và C.

## 3. Data Contract — KHÔNG ĐƯỢC THAY ĐỔI

data/spaces.json là array object với tất cả field bắt buộc:
- id: unique string
- name: string
- district: string
- address: string
- type: cafe | library | coworking
- pricePerHour: non-negative integer, VND
- noiseLevel: quiet | moderate | lively
- amenities: array of wifi | outlet | ac | parking
- hours: string
- description: string

pricePerHour = 0 nghĩa là miễn phí.

Không tự ý thay tên field hoặc thêm thuộc tính bắt buộc.

## 4. Public API Contract — KHÔNG ĐƯỢC THAY ĐỔI

Module B:
assets/js/components/space-cards.js

Named exports:
- createSpaceCard(space, { isFavorite, onViewDetail, onToggleFavorite }) trả về HTMLElement.
- openSpaceDetails(space, { isFavorite, onToggleFavorite }) hiển thị chi tiết.

Callback:
- onViewDetail(id) nhận ID địa điểm.
- onToggleFavorite(id) trả về boolean thể hiện trạng thái yêu thích mới.

Module C:
assets/js/features/favorites.js

Named exports:
- getFavoriteIds() trả về string[].
- toggleFavorite(id) trả về string[] sau cập nhật.
- renderFavoritesToolbar(container, { count, showOnlyFavorites, onToggle }) tạo/cập nhật thanh lọc yêu thích.

Module A thực hiện:
- Import module B và C khi đã có.
- Kết nối callback của B với toggleFavorite của C.
- Sau khi thay đổi yêu thích, cập nhật card, modal, toolbar và danh sách nếu đang bật lọc yêu thích.
- Không import hàm nội bộ chưa export.
- Không tạo bản sao độc lập của favorites trong app.js.

## 5. File thuộc phạm vi của bạn

- index.html
- .nojekyll
- assets/css/base.css
- assets/js/app.js
- assets/js/search.js
- docs/CONTRACT.md
- docs/ARCHITECTURE.md
- docs/UX-RESEARCH.md
- docs/WORKLOG-A.md

Không sửa file của B hoặc C khi đang phát triển song song.

## 6. Công việc kỹ thuật

Tạo:
- Header với nhận diện Study Space Finder.
- Hero section và thanh tìm kiếm.
- Bộ lọc theo khu vực, loại địa điểm, giá, độ ồn, tiện ích.
- Hiển thị bộ lọc đang được áp dụng và nút xóa.
- Số kết quả.
- Sắp xếp giá tăng/giảm và tên.
- Grid địa điểm.
- Loading, error và empty state.
- Responsive layout.
- Footer.

Viết logic:
- Tải ./data/spaces.json bằng fetch.
- Tìm kiếm tiếng Việt không dấu.
- Các nhóm điều kiện lọc kết hợp đúng logic.
- Không làm thay đổi dữ liệu gốc khi sắp xếp.
- Kết nối với module B/C sau khi được merge.

Trong lúc B/C chưa hoàn thiện, triển khai và test phần A độc lập. Không tạo file giả trùng tên module của họ. Nếu chức năng phải chờ tích hợp, đánh dấu BLOCKED thay vì tuyên bố hoàn tất.

## 7. Quy chuẩn UI/UX

Ưu tiên nghiên cứu có căn cứ:
- Baymard Institute: https://baymard.com/research-articles/current-state-product-list-and-filtering
- Baymard applied filters: https://baymard.com/research-articles/how-to-design-applied-filters
- Airbnb UX benchmark: https://baymard.com/ux-benchmark/case-studies/airbnb
- Nielsen Norman Group: https://www.nngroup.com/articles/ten-usability-heuristics/
- WCAG 2.2: https://www.w3.org/TR/WCAG22/
- Google Core Web Vitals: https://web.dev/articles/vitals

Ghi nguồn đã đọc trong UX-RESEARCH.md, nêu lý do áp dụng và mức độ bằng chứng. Không tự tạo thống kê hoặc khẳng định một website tối ưu khi chưa có dữ liệu.

Phong cách: sạch, hiện đại, dễ đọc, phù hợp sinh viên. Chọn một bộ màu và typography thống nhất, có responsive, focus visible, accessibility và contrast tốt.

Mục tiêu Lighthouse Performance/Accessibility >=90, nhưng chỉ ghi PASS khi đã đo thực tế.

## 8. Quy định CSS và đường dẫn

- Chỉ module A quản lý global styles, design tokens và layout chính.
- Không dùng selector thay đổi trực tiếp các component của B/C.
- B dùng class .space-card-*, .space-detail-*, .sp-*.
- C dùng class .fav-*.
- Trong index.html, kết nối đủ 3 file CSS sau khi tích hợp.
- JavaScript sử dụng type="module".
- Tài nguyên dùng relative paths để hoạt động trên GitHub Pages project subpath.

## 9. Git và phối hợp nhóm

Sau base commit:
- Phát triển phần A trên feature/core.
- Kiểm tra branch trước khi commit/push.
- Tạo commit mô tả công việc thật.
- Không merge nhánh B/C khi chưa được người dùng yêu cầu.
- Không sửa hoặc hoàn thành thay nhiệm vụ của đồng đội.

Trước khi push, kiểm tra file thay đổi chỉ thuộc phạm vi A.

## 10. Ghi nhật ký và học tập

Cập nhật WORKLOG-A.md:
- Công việc đã hoàn thành.
- Đường dẫn file thay đổi.
- Lệnh đã thực sự chạy và tác dụng.
- Git branch và commit.
- Cách hoạt động của các hàm chính.
- Lỗi thực tế và cách xử lý.
- Kiểm thử PASS/FAIL/BLOCKED/NOT RUN.
- Ít nhất 10 câu hỏi thầy có thể hỏi và câu trả lời dễ hiểu.

Không bịa kết quả đo, lệnh terminal hay commit.

## 11. Quy trình thực thi

BƯỚC A0: Tạo contract và base commit trên main.

BƯỚC A1: Tạo branch feature/core và phát triển module A.

BƯỚC A2: Kiểm thử riêng, hoàn thiện tài liệu, push branch.

BƯỚC A3: Báo trạng thái sẵn sàng tích hợp, chờ người dùng yêu cầu ghép.

Khi gặp lỗi:
- Phân tích và nêu file/hàm gây lỗi.
- Đưa phương án sửa thuộc đúng module.
- Nếu lỗi vượt phạm vi A, đề xuất giao lại cho người phụ trách, không tự làm thay.
- Trước thay đổi contract, phải được người dùng phê duyệt.

BẮT ĐẦU NGAY: Kiểm tra repo hiện tại, thực hiện BƯỚC A0, rồi thực hiện các phần tiếp theo trong phạm vi được phép. Nếu GitHub chưa được xác thực, hoàn thành nội dung local có thể làm và báo rõ bước cần người dùng thao tác.
```

### Prompt B — Thành viên 2: Dữ liệu, card, chi tiết địa điểm

> **Dán nguyên prompt này vào Antigravity Agent của người B sau khi A đã push base contract.**

```text
# ANTIGRAVITY — STUDY SPACE FINDER — MEMBER B

VAI TRÒ: Frontend Developer — Data & Space Cards.

Bạn phụ trách module B trong dự án đồ án cuối kỳ Study Space Finder, gồm 3 thành viên làm việc với Antigravity trên 3 máy trường.

MỤC TIÊU CHUNG:
Website tìm kiếm không gian học tập dành cho sinh viên, dùng HTML5, CSS3, JavaScript ES Modules, JSON và GitHub Pages.

KHÔNG xây dựng lại toàn bộ website. KHÔNG thay đổi kiến trúc của trưởng nhóm. KHÔNG tự ý sử dụng framework hoặc thêm backend.

## 1. Bắt đầu

- Mở repository chung trong Antigravity.
- Kiểm tra đang làm đúng GitHub repository.
- Đọc docs/CONTRACT.md.
- Xác nhận base commit đã tồn tại trên main.
- Cập nhật từ main và tạo branch feature/space-cards.
- Không viết code trên main.
- Nếu contract chưa có hoặc không khớp quy định bên dưới, dừng chỉnh sửa và báo người dùng.

## 2. Chỉ sở hữu các file

- data/spaces.json
- assets/js/components/space-cards.js
- assets/css/space-cards.css
- docs/WORKLOG-B.md

Không chỉnh sửa index.html, app.js, search.js, favorites.js hoặc bất cứ file nào của người khác.

## 3. Dữ liệu

Tạo ít nhất 12 địa điểm mẫu đa dạng cho sinh viên.

Mỗi object trong JSON bắt buộc có:
- id: unique string
- name: string
- district: string
- address: string
- type: cafe | library | coworking
- pricePerHour: non-negative integer, VND
- noiseLevel: quiet | moderate | lively
- amenities: array gồm wifi | outlet | ac | parking
- hours: string
- description: string

Không đổi field và enum.

Phải có địa điểm miễn phí, mức giá khác nhau, loại địa điểm khác nhau, khu vực khác nhau và tiện ích đa dạng để bộ lọc của module A có thể kiểm thử.

Nội dung bằng tiếng Việt tự nhiên.

Nếu chưa xác minh được địa điểm thực tế, dùng dữ liệu minh họa và ghi rõ là DEMO. Không bịa đánh giá, review thật, giờ mở cửa thực tế hoặc ảnh giả được trình bày như ảnh địa điểm thật.

## 4. Public API cố định

Trong space-cards.js, chỉ cần export đúng hai named functions:

createSpaceCard(space, { isFavorite, onViewDetail, onToggleFavorite })

Hàm phải:
- Tạo và trả về HTMLElement.
- Hiển thị tên, khu vực, loại, giá, độ yên tĩnh và tiện ích.
- Có nút xem chi tiết.
- Khi bấm xem chi tiết gọi onViewDetail(space.id).
- Khi bấm yêu thích gọi onToggleFavorite(space.id).
- Callback trả về boolean trạng thái mới.
- Cập nhật aria-pressed và trạng thái giao diện.
- Không tự đọc/ghi localStorage.
- Không import module A hoặc C.

openSpaceDetails(space, { isFavorite, onToggleFavorite })

Hàm phải:
- Mở dialog chi tiết của địa điểm.
- Hiển thị đầy đủ mô tả, địa chỉ, giờ, giá, tiện ích.
- Có nút lưu yêu thích sử dụng callback trên.
- Đóng bằng nút X, phím Escape và click backdrop.
- Quản lý focus khi mở/đóng.
- Không tạo nhiều dialog hoặc event listener trùng.

Không thay chữ ký hàm.

## 5. UI/UX

Thiết kế card hiện đại, đồng bộ với design tokens trong base.css.

Tham khảo các nguyên tắc thẻ địa điểm, phân cấp thông tin, khả năng quét nhanh và accessibility. Không lấy giao diện nổi tiếng làm bằng chứng rằng thiết kế tốt.

- Tên rõ, không bị cắt mất phần quan trọng.
- Giá có đơn vị.
- Các biểu tượng có accessible label.
- Hover, active, focus states.
- Giao diện desktop và mobile.
- Nếu chưa có ảnh hợp lệ, dùng placeholder CSS/SVG.
- Không copy ảnh có bản quyền hoặc gắn ảnh không đúng địa điểm.

CSS chỉ sử dụng các prefix:
- .space-card-*
- .space-detail-*
- .sp-*

Không đặt global selector cho body, header, button, main.

## 6. Kiểm thử

Kiểm tra dữ liệu:
- JSON hợp lệ.
- Ít nhất 12 địa điểm.
- ID duy nhất.
- Không thiếu field.
- Giá là number.
- Enum đúng.

Kiểm tra component:
- Trả về HTMLElement.
- Nút xem chi tiết gọi đúng callback.
- Nút yêu thích cập nhật trạng thái.
- Dialog mở/đóng đúng.
- Không import sai hoặc lỗi JavaScript.
- Không làm lỗi giao diện mobile.

Nếu chưa có module A hoàn chỉnh, kiểm thử trong phạm vi module B. Không tự tạo file đè lên module A để chạy test.

## 7. Nhật ký

Tạo WORKLOG-B.md ghi:
- Các file đã viết.
- Tên và chức năng từng hàm.
- Vì sao dùng JSON.
- Cách tạo DOM bằng JavaScript.
- Cách event listeners hoạt động.
- Lệnh terminal thực sự đã chạy.
- Lỗi thực tế và cách xử lý.
- Kết quả kiểm thử thật.
- Ít nhất 8 câu hỏi thầy có thể hỏi cùng câu trả lời ngắn.

## 8. Bàn giao

- Kiểm tra git status.
- Commit bằng tài khoản/định danh của thành viên đang làm thực tế.
- Push branch feature/space-cards.
- Tạo Pull Request từ feature/space-cards vào main nếu có quyền.
- Không tự merge.
- Không thay đổi bất kỳ file sở hữu bởi người khác.

Nếu push hoặc đăng nhập GitHub thất bại:
- Không xóa code.
- Tạo file study-space-finder-member-B.zip.
- ZIP chỉ chứa 4 file được giao với đúng cấu trúc thư mục.
- Không chứa .git, dữ liệu cá nhân, cache hay file rác.
- Hướng dẫn người dùng giải nén và upload các file đó lên branch riêng bằng GitHub web.

KẾT QUẢ CUỐI:
Module B có thể được ghép vào website bằng các export đã thống nhất, có worklog đầy đủ và có thể giải thích trước giảng viên.

Hãy kiểm tra repo rồi bắt đầu thực hiện đúng phạm vi B.
```

### Prompt C — Thành viên 3: Yêu thích, QA, tài liệu

> **Dán nguyên prompt này vào Antigravity Agent của người C sau khi A đã push base contract.**

```text
# ANTIGRAVITY — STUDY SPACE FINDER — MEMBER C

VAI TRÒ: Frontend Developer — Favorites, Testing & Documentation.

Bạn là thành viên thứ 3 của đồ án Study Space Finder. Nhóm sử dụng Antigravity trên các máy trường khác nhau và đồng bộ source bằng GitHub.

MỤC TIÊU CHUNG:
Website tìm kiếm không gian học tập cho sinh viên, có bộ lọc, xem chi tiết và lưu địa điểm yêu thích. Website phải chạy được trên GitHub Pages.

Sử dụng HTML5, CSS3, JavaScript ES Modules và localStorage. Không thêm backend, framework, package hoặc database.

## 1. Bắt đầu

- Mở repository nhóm trong Antigravity.
- Đọc docs/CONTRACT.md.
- Xác nhận dự án đã có bản nền trên main.
- Tạo branch feature/favorites-qa từ main mới nhất.
- Không làm việc trực tiếp trên main.
- Không viết lại website.

## 2. Các file sở hữu

- assets/js/features/favorites.js
- assets/css/favorites.css
- README.md
- docs/WORKLOG-C.md
- docs/TEST-REPORT.md
- docs/DEFENSE-NOTES.md

Không sửa app.js, index.html, search.js, space-cards.js, spaces.json và file của người khác.

## 3. Public API cố định

Export đúng 3 named functions trong favorites.js:

getFavoriteIds()
- Trả về string[] chứa các ID đã lưu.
- Loại bỏ ID trùng.
- Xử lý dữ liệu localStorage bị hỏng hoặc không thể truy cập.
- Không làm ứng dụng crash.

toggleFavorite(id)
- Nhận ID dạng string.
- Chưa có thì thêm.
- Đã có thì bỏ.
- Lưu danh sách mới.
- Trả về string[] sau thay đổi.
- Nếu không thể dùng localStorage, dùng fallback bộ nhớ phiên hiện tại và báo rõ giới hạn đó.

renderFavoritesToolbar(container, { count, showOnlyFavorites, onToggle })
- Nhận một HTMLElement container.
- Hiển thị số lượng yêu thích.
- Tạo nút "Chỉ hiện yêu thích".
- Thể hiện đúng trạng thái đang bật/tắt.
- Khi click gọi onToggle().
- Không trực tiếp sửa mảng địa điểm.
- Không tự lọc danh sách hoặc import module A/B.
- Không tạo listener trùng khi render lại.

Storage key cố định:
study-space-finder:favorites:v1

Không đổi chữ ký hàm và kiểu dữ liệu trả về.

## 4. Giao diện

- Toolbar nhỏ, gọn, dễ thao tác.
- Có biểu tượng trái tim.
- Hiển thị tổng số yêu thích.
- Có trạng thái bật/tắt rõ ràng.
- Hỗ trợ aria-pressed và keyboard.
- Hoạt động trên màn hình điện thoại.
- CSS chỉ sử dụng prefix .fav-*.
- Dùng design tokens từ base.css.

## 5. Kiểm thử module

Chuẩn bị test cho:
1. Danh sách trống.
2. Thêm địa điểm.
3. Bỏ địa điểm.
4. Thêm nhiều địa điểm.
5. Không xuất hiện ID trùng.
6. Refresh vẫn lưu dữ liệu.
7. localStorage chứa JSON lỗi.
8. localStorage không khả dụng.
9. Chỉ hiện các địa điểm yêu thích.
10. Toolbar thể hiện đúng số lượng và trạng thái.
11. Thao tác bằng bàn phím.
12. Không có lỗi runtime đã biết.

Nếu module A hoặc B chưa có, ghi test tích hợp là BLOCKED/NOT RUN thay vì tuyên bố PASS.

## 6. Tài liệu

README.md gồm:
- Giới thiệu dự án.
- Chức năng.
- Công nghệ.
- Hướng dẫn chạy website bằng local HTTP server.
- Hướng dẫn GitHub Pages.
- Phân công 3 thành viên dưới dạng placeholder để nhóm điền chính xác.
- Những giới hạn của dữ liệu demo.

WORKLOG-C.md:
- Công việc đã thực hiện.
- File đã thay đổi.
- Lệnh thực sự đã dùng.
- Commit.
- Giải thích code.
- Lỗi và giải pháp.
- Kiến thức cần nắm.

TEST-REPORT.md:
- Test case.
- Expected result.
- Actual result.
- Trạng thái PASS/FAIL/BLOCKED/NOT RUN.
- Trình duyệt, thiết bị và thời điểm thử nghiệm.
- Các lỗi cần chuyển cho đúng thành viên xử lý.

DEFENSE-NOTES.md:
- Câu hỏi và đáp án về HTML, CSS, JS.
- JSON và localStorage.
- DOM và sự kiện.
- Git, GitHub, branch, Pull Request.
- GitHub Pages.
- Responsive và accessibility.
- Giải thích các chức năng chính.
- Ít nhất 15 câu hỏi có đáp án ngắn.
- Phân biệt dữ liệu demo và thông tin đã xác minh.

Không tự bịa kết quả kiểm thử, lịch sử code hoặc câu trả lời không đúng với code thực tế.

## 7. Giai đoạn sau khi tích hợp

Khi trưởng nhóm thông báo website đã merge:
- Cập nhật workspace theo main mới.
- Đọc code mới nhất trước khi test.
- Kiểm tra các chức năng được giao và giao diện chung.
- Thử website tại localhost và GitHub Pages nếu có.
- Ghi kết quả thực tế trong TEST-REPORT.md.
- Nếu lỗi thuộc module khác, ghi rõ bước tái hiện, thông báo lỗi, file/hàm nghi ngờ và gửi cho đúng người phụ trách.
- Không sửa thay module của người khác.

Các cập nhật tài liệu sau merge phải được commit lên một branch mới hoặc branch còn phù hợp, rồi tạo Pull Request riêng.

## 8. Bàn giao GitHub

- Kiểm tra branch hiện tại.
- Commit đúng file được giao.
- Push lên feature/favorites-qa.
- Tạo Pull Request vào main nếu có quyền.
- Không tự merge.

Nếu không thể push:
- Tạo study-space-finder-member-C.zip.
- ZIP chứa đúng các file sở hữu, giữ nguyên đường dẫn.
- Không có file .git hoặc file rác.
- Hướng dẫn thành viên giải nén rồi upload source lên branch riêng qua GitHub web.

KẾT QUẢ CUỐI:
Module yêu thích hoạt động đúng contract, có bộ kiểm thử và tài liệu hỗ trợ nhóm bảo vệ đồ án.

Bắt đầu bằng việc kiểm tra repo, đọc CONTRACT.md và triển khai module C.
```

**Cách gửi:** Mỗi người chỉ nhận đúng prompt của mình. Cả ba cần clone cùng repository và đọc `docs/CONTRACT.md` từ cùng một base commit, chứ không dùng 3 bộ mô tả chung độc lập. Các thay đổi hợp đồng sau đó phải được các thành viên thống nhất.

---
## 6. Hai cách đưa code lên GitHub: push hoặc ZIP

### Cách 1 — Antigravity tự commit và push lên branch riêng (ưu tiên)

Sau khi clone repo, mỗi người mở **Terminal → New Terminal** trong Antigravity ở thư mục gốc dự án. Người B dùng:

```powershell
git switch main
git pull origin main
git switch -c feature/space-cards
```

Sau khi hoàn tất module B, người B dùng:

```powershell
git status
git add data/spaces.json
git add assets/js/components/space-cards.js
git add assets/css/space-cards.css
git add docs/WORKLOG-B.md
git diff --cached --stat
git commit -m "Add study space cards and dataset"
git push -u origin feature/space-cards
```

- **A:** dùng branch `feature/core` (sau khi đã tạo base contract trên `main`).
- **B:** dùng branch `feature/space-cards`.
- **C:** dùng branch `feature/favorites-qa`.
- Mỗi người chỉ `git add` những file được giao. Tránh `git add .` khi chưa xem toàn bộ `git status` trên máy dùng chung.
- Các lệnh này chạy trong **terminal của Antigravity**, không phải ô chat Agent. Agent cũng có thể thực hiện sau khi được người dùng phê duyệt.

Khi push xong: trên GitHub mở branch → **Compare & pull request** → **base `main`**, **compare branch người đó** → **Create pull request**. Không tự merge khi chưa được review. Nếu branch đã tồn tại, không chạy lại `git switch -c` mà chuyển đúng branch rồi cập nhật nó.

**Danh tính commit:** mỗi thành viên dùng tài khoản GitHub riêng và đặt `user.name`/`user.email` phù hợp trên từng repo. Ví dụ lệnh (thay bằng danh tính thật của người đang làm):

```powershell
git config --local user.name "TEN_THANH_VIEN"
git config --local user.email "EMAIL_DA_XAC_NHAN_TREN_GITHUB"
```

`user.name`/`user.email` **chỉ là thông tin tác giả commit**, không phải cơ chế đăng nhập hay cấp quyền push. GitHub cần xác thực riêng qua trình duyệt/Git Credential Manager/GitHub CLI/PAT/SSH tùy môi trường. Không dùng chung tài khoản để giả lịch sử đóng góp.

### Cách 2 — Antigravity đóng gói ZIP, thành viên upload qua website GitHub

Dùng khi máy trường không cho push hoặc có lỗi đăng nhập GitHub:

1. Trong Antigravity, yêu cầu Agent xuất ZIP **chỉ các file thuộc người đó**, bảo toàn đường dẫn tương đối, không chứa `.git`, file cache, mật khẩu hay thư mục rác.
2. Ví dụ ZIP người B là `study-space-finder-member-B.zip` có nội dung:

   ```text
   assets/
     css/
       space-cards.css
     js/
       components/
         space-cards.js
   data/
     spaces.json
   docs/
     WORKLOG-B.md
   ```

3. **Giải nén** ZIP trên máy trường. GitHub web **không tự giải nén ZIP thành source code**.
4. Vào repository → tạo/chọn branch **của thành viên** xuất phát từ `main`, không upload thẳng lên `main`.
5. Chọn **Add file → Upload files**, kéo các thư mục/file đã giải nén vào trang upload. Kiểm tra **đường dẫn chính xác**. Trong một số giao diện hoặc trình duyệt, nếu kéo cả thư mục không hoạt động, chọn file và dùng cách upload có thể giữ cấu trúc đường dẫn, hoặc gửi ZIP cho trưởng nhóm tích hợp bằng Git.
6. Ghi commit message và commit vào branch của mình.
7. Tạo Pull Request từ branch của mình vào `main` để trưởng nhóm review.

Giới hạn web upload hiện được GitHub công bố: tối đa **100 file mỗi lần** và **25 MiB cho mỗi file**. Nếu upload qua web khó hoặc mất cấu trúc, dùng Git trên máy có quyền hoặc nhờ trưởng nhóm tích hợp ZIP, nhưng phải ghi nhận đúng người thực hiện code. **Một commit upload do trưởng nhóm thực hiện không tự động chứng minh người khác đã tạo ra mã nguồn.**

**Tránh sai thư mục:** không để `study-space-finder/study-space-finder/assets/...`. File `index.html` phải ở root; `README.md` và `data/` cũng nằm ngay dưới root đúng như cây thư mục.

---

## 7. Ghép code và cho Antigravity kiểm tra web

### Review và merge

Sau khi B và C gửi Pull Request, trưởng nhóm xem nội dung thay đổi, so sánh với `CONTRACT.md`, xác nhận đúng file sở hữu và API. Merge module B/C và phần A vào `main` theo tình trạng PR cụ thể. **Không có thứ tự merge cố định nào thay thế được việc review thực tế**; điều quan trọng là kiểm tra trạng thái tích hợp sau từng merge.

### Cho Antigravity đọc toàn bộ source mới nhất

Trên máy trường của trưởng nhóm, nếu chưa clone repo:

```powershell
git clone https://github.com/USERNAME/study-space-finder.git
cd study-space-finder
git switch main
git pull origin main
```

Nếu thư mục đã tồn tại thì **không clone lồng bên trong**: chọn Open Folder đúng thư mục repo, kiểm tra `git status`, `git remote -v`, sau đó cập nhật `main` khi an toàn. Với local changes chưa commit, không chạy pull bừa bãi.

Mở thư mục đó trong Antigravity bằng **Open Folder** hoặc **New Project → Add Folder**. Khi đã clone/pull đầy đủ, Agent mới có nội dung của cả ba module để đọc và kiểm tra. **Kết nối tài khoản GitHub không tự làm cho mọi file trên mạng xuất hiện trong workspace**; phải clone/pull hoặc có tích hợp đọc repo thích hợp.

### Mở web local

Terminal trong Antigravity, tại thư mục gốc dự án, chạy:

```powershell
py -m http.server 5500
```

Mở `http://localhost:5500/`. Nếu máy trường thiếu Python, hãy yêu cầu Antigravity tìm phương án HTTP server **có sẵn và được phép**, không tự cài phần mềm hoặc sửa hệ thống của trường khi chưa được phép.

Không chỉ mở `index.html` bằng `file://`: ES Modules và `fetch` JSON có thể bị giới hạn bởi trình duyệt. Nếu browser agent có quyền, yêu cầu mở trang, thao tác, kiểm tra Console/Network và giao diện ở nhiều kích thước. Nếu browser automation không có sẵn, phải ghi test chưa chạy rồi người dùng kiểm thử thủ công.

### Triển khai GitHub Pages

Trong GitHub repository vào **Settings → Pages**:

1. **Build and deployment → Source:** `Deploy from a branch`.
2. **Branch:** `main`.
3. **Folder:** `/ (root)`.
4. Chọn **Save**.
5. Kiểm tra báo cáo workflow/deploy của GitHub; nếu thành công, đường dẫn có dạng:

   `https://USERNAME.github.io/study-space-finder/`

Đây là ví dụ; thay `USERNAME` bằng tài khoản GitHub thật. Với GitHub Pages dạng project site, các đường dẫn asset phải là đường dẫn **tương đối** (`./assets/...`, `./data/...`) để tránh lỗi trang chủ chạy nhưng tài nguyên 404.

---

## 8. Prompt kiểm tra tích hợp, tự đề xuất người sửa

> **Chỉ dùng prompt này khi cả 3 phần đã được merge vào `main`. Người dùng yêu cầu Antigravity tự đề xuất phân công lỗi sau audit; tài liệu này không tự tạo một bảng phân công lỗi trước khi thấy vấn đề thực tế.**

```text
# ANTIGRAVITY — FINAL INTEGRATION AUDIT & REPAIR ASSIGNMENT

Bạn là Technical Lead và QA Engineer đang kiểm tra phiên bản hoàn chỉnh của đồ án Study Space Finder.

Website được xây dựng bởi 3 thành viên trên 3 máy trường khác nhau, dùng chung một GitHub repository. Các module đã được merge vào main.

NHIỆM VỤ CỦA BẠN: Đọc toàn bộ code, chạy website thật, đánh giá chất lượng, xác định lỗi và lập phân công sửa lỗi hợp lý dựa trên phạm vi của từng thành viên.

## 1. Đọc toàn bộ source

Trước tiên:
- Xác nhận workspace là repository đúng.
- Kiểm tra git status, remote, branch.
- Fetch/pull phiên bản main mới nhất khi được phép.
- Đọc cấu trúc thư mục và mọi file liên quan.
- Đọc CONTRACT.md và ARCHITECTURE.md.
- Đọc ba WORKLOG của nhóm.
- Kiểm tra import/export, data schema, localStorage và đường dẫn asset.

Không được kết luận mọi thứ hoạt động chỉ vì file tồn tại.

## 2. Chạy website

- Khởi động local HTTP server.
- Mở localhost trong browser agent nếu khả dụng.
- Nếu có thể, mở cả website GitHub Pages.
- Kiểm tra browser console và network.
- Kiểm tra các lỗi 404, dữ liệu JSON, CSS và JavaScript.
- Thao tác trực tiếp với website, không chỉ đọc code.

Nếu môi trường không cho phép browser automation, nói rõ giới hạn và hướng dẫn người dùng mở Chrome để kiểm tra. Không tự tuyên bố đã xem giao diện nếu chưa thực hiện.

## 3. Kiểm thử chức năng

Thực hiện:
1. Trang chủ tải đúng.
2. Dữ liệu địa điểm xuất hiện.
3. Tìm tên địa điểm.
4. Tìm tiếng Việt không dấu.
5. Lọc theo khu vực.
6. Lọc theo giá.
7. Lọc theo độ yên tĩnh.
8. Lọc theo tiện ích.
9. Kết hợp nhiều bộ lọc.
10. Xóa bộ lọc.
11. Sắp xếp.
12. Mở chi tiết.
13. Đóng dialog.
14. Lưu yêu thích.
15. Bỏ yêu thích.
16. Chỉ hiển thị yêu thích.
17. Refresh vẫn giữ dữ liệu.
18. Empty state.
19. Responsive mobile, tablet và desktop.
20. Keyboard navigation và focus.

Phải ghi PASS/FAIL/BLOCKED/NOT RUN cho từng trường hợp.

## 4. Kiểm tra UI/UX

Không đánh giá theo cảm tính đơn thuần.

Đánh giá dựa trên:
- Bố cục và phân cấp thông tin.
- Khả năng tìm thấy chức năng.
- Tính nhất quán.
- Mobile usability.
- Khả năng đọc, contrast, keyboard.
- Thông báo lỗi và phản hồi thao tác.
- Mức độ tập trung vào nhu cầu sinh viên.

Nếu có công cụ, đo Lighthouse và các chỉ số hiệu năng. Chỉ ghi số đo có thật.

Tham khảo nghiên cứu Baymard, NN/g, WCAG và Core Web Vitals; không tự bịa dữ liệu.

## 5. Tìm nguyên nhân lỗi

Với mỗi lỗi:
- Mô tả triệu chứng.
- Cách tái hiện.
- File/hàm liên quan.
- Nguyên nhân đã xác nhận hoặc giả thuyết cần kiểm tra.
- Mức độ ảnh hưởng.
- Bằng chứng từ Console, Network, ảnh hoặc test.
- Cách sửa đề xuất.
- Điều kiện xác nhận đã sửa.

Không sửa theo kiểu thử ngẫu nhiên hàng loạt.

## 6. TỰ PHÂN CHIA CÔNG VIỆC SỬA

Dựa trên CONTRACT.md và phạm vi file của nhóm, bạn tự xác định lỗi nào thuộc người 1, người 2 hoặc người 3.

Quy tắc:
- Không thay đổi phân công gốc.
- Lỗi giao diện tổng thể, search, filter, integration thuộc phạm vi người 1.
- Lỗi dataset, card, modal thuộc người 2.
- Lỗi favorites, tài liệu và kiểm thử thuộc người 3.
- Nếu lỗi liên quan nhiều module, chỉ định một người chịu trách nhiệm chính, xác định phần hỗ trợ cần thiết.
- Không giao người khác sửa file mà họ không sở hữu.
- Không tự ý sửa mọi module thay cả nhóm.
- Đề xuất mức ưu tiên, thứ tự xử lý và test nghiệm thu cho từng lỗi.

Hãy tự đưa ra phân công dựa trên kết quả audit, không yêu cầu người dùng tự phân tích lỗi.

## 7. Tạo báo cáo kiểm tra

Tạo docs/INTEGRATION-AUDIT.md (file báo cáo do trưởng nhóm quản lý), gồm:
- Ngày, phiên bản/commit được kiểm tra.
- Danh sách file đã đọc.
- Cách website được chạy.
- URL đã kiểm tra.
- Danh sách test và kết quả.
- Lỗi, bằng chứng và nguyên nhân.
- Đề xuất phân công sửa.
- Những phần chưa thể kiểm thử.
- Kết luận về trạng thái website.

Không sửa vào file của các thành viên nếu chỉ được yêu cầu audit.

Nếu toàn bộ bài kiểm tra hoàn thành, báo rõ website có đáp ứng mục tiêu hay không và những điểm cần cải thiện.

Nếu lỗi vẫn còn, đưa ra các nhiệm vụ sửa độc lập để trưởng nhóm gửi cho đúng Antigravity của từng thành viên.

BẮT ĐẦU BẰNG VIỆC ĐỌC REPOSITORY HIỆN TẠI VÀ CHẠY WEBSITE THỰC TẾ.
```

---

## 9. Checklist và lưu ý

- [ ] Trưởng nhóm tạo repository và mời hai thành viên.
- [ ] Trưởng nhóm chạy Prompt A, tạo `CONTRACT.md`, push base commit.
- [ ] Hai thành viên clone cùng repository, xác nhận base commit, tạo branch riêng.
- [ ] Ba người chạy Antigravity Agent theo prompt được giao, chỉ sửa đúng file.
- [ ] Mỗi thành viên push branch hoặc xuất ZIP và upload file source lên branch.
- [ ] Trưởng nhóm review Pull Request và merge.
- [ ] Antigravity của trưởng nhóm clone/pull đủ file, mở và kiểm tra website.
- [ ] Antigravity đề xuất phân công sửa lỗi dựa trên audit, không tự sửa thay cả nhóm.
- [ ] Các thành viên sửa lỗi, kiểm thử lại.
- [ ] Website được triển khai thành công trên GitHub Pages và URL được kiểm tra thật.
- [ ] Nhóm lưu worklog, lệnh code, commit, test report và câu hỏi bảo vệ.

### Những điều cần tránh

- Không dùng chung một tài khoản GitHub để chứng minh đóng góp của cả ba.
- Không cho Agent chạy `git push --force` hoặc thao tác xóa hàng loạt không có review.
- Không tự sửa `CONTRACT.md` khi các thành viên đang code dựa trên contract cũ.
- Không bật cấp quyền terminal/file ngoài workspace vô hạn trên máy trường.
- Không chạy lại `git clone` trong một thư mục đã clone sẵn.
- Không xem ZIP nguyên vẹn là source đã được upload lên GitHub; ZIP phải được giải nén và các file phải xuất hiện đúng vị trí.
- Không khẳng định đã đạt Lighthouse hoặc tất cả test PASS nếu chưa kiểm tra thật.

---

## 10. Giải đáp: Có cần kết nối GitHub để prompt chính xác nhất không?

**Có thể kết nối Antigravity với GitHub qua Git, và đây là phương án nên dùng. Tuy nhiên, chỉ kết nối GitHub không tự bảo đảm AI làm đúng.** Để ba Agent ra đúng một sản phẩm, cần đồng thời:

1. **Cùng source và cùng bản nền:** mỗi người clone cùng repo, base branch `main` chứa `docs/CONTRACT.md` và cùng một commit ban đầu.
2. **Hợp đồng kỹ thuật cố định:** schema JSON, tên file, public API, design tokens, CSS prefixes và phạm vi file rõ ràng. Prompt yêu cầu đọc contract trước khi code.
3. **Mỗi người một branch:** Agent chỉ sửa file sở hữu, commit/push, tạo Pull Request. Trưởng nhóm review từng diff.
4. **Kiểm chứng thật:** Agent phải chạy test trên phần mình, ghi các bước chưa chạy, và trưởng nhóm phải kiểm tra tích hợp cuối cùng bằng browser.
5. **Không phụ thuộc máy trường:** code ở GitHub, worklog ở repository; sang máy khác chỉ cần clone/pull đúng branch.

### Antigravity kết nối GitHub bằng cách nào?

Antigravity **không bắt buộc phải có nút “Connect GitHub” đặc biệt** để làm được dự án. Antigravity nhận diện **Git repository trong Project/workspace** và có terminal hoặc giao diện VCS để xem thay đổi, stage, commit. Việc push sử dụng cơ chế Git/GitHub của máy đang dùng.

**Cách A — Dễ nhất, nếu Antigravity IDE có “Clone Repository”:**

1. Trên GitHub repo, bấm **Code → HTTPS** → copy URL.
2. Mở Antigravity → **Clone Repository** → dán URL.
3. Chọn vị trí thư mục được phép ghi trên máy trường.
4. Mở repository trong workspace.
5. Mở Terminal và chạy `git remote -v`, `git status`, `git branch --show-current` để biết Agent đang ở đúng repo/branch.
6. Tạo branch của mình và code. Khi push, thực hiện xác thực GitHub nếu trình duyệt/credential manager yêu cầu.

**Cách B — Không có nút Clone:**

Trong **Terminal của Antigravity**:

```powershell
git --version
git clone https://github.com/USERNAME/study-space-finder.git
cd study-space-finder
git remote -v
git status
git branch --show-current
```

Sau đó mở thư mục bằng **Open Folder** hoặc **New Project → Add Folder**. Không cần thêm plugin GitHub riêng để sử dụng Git CLI thông thường.

**Cách xác thực để push** (chỉ dùng phương thức được máy trường cho phép):

- Nếu có **Git Credential Manager**, khi `git push`, máy có thể mở cửa sổ trình duyệt để xác thực tài khoản GitHub. Chấp thuận trên tài khoản của chính mình.
- Nếu đã cài **GitHub CLI**, có thể chạy `gh auth login`, chọn GitHub.com, HTTPS và đăng nhập qua trình duyệt; sau đó dùng `git push`.
- Nếu những cách trên không có, GitHub hỗ trợ **Personal Access Token** làm thông tin xác thực HTTPS thay cho mật khẩu; không gửi token cho AI và không lưu nó trong mã nguồn hay URL remote. Trên máy chung, không nên dùng token dài hạn và phải đăng xuất/thu hồi khi cần.
- Nếu trường chặn hoàn toàn xác thực Git, sử dụng **ZIP → upload qua trình duyệt** như mục 6.

**Quan trọng:** Google Account dùng đăng nhập Antigravity **không phải** giấy phép truy cập vào repo GitHub riêng tư và không cấp quyền `git push`. Thành viên cần được mời vào repository hoặc có quyền write phù hợp, đồng thời xác thực GitHub đúng tài khoản.

### Một prompt khởi động ngắn để cả ba Agent không lệch mục tiêu

Trước prompt A/B/C, có thể dán lời dẫn sau (thay `ROLE` bằng A, B, C):

```text
Bạn đang làm thành viên ROLE của dự án Study Space Finder trên máy trường.
Trước khi code, đọc toàn bộ docs/CONTRACT.md trong workspace Git hiện tại.
Kiểm tra git remote -v, git branch --show-current, git status và base commit của main.
Tóm tắt đúng 5 điều: mục tiêu sản phẩm, data schema, public API, file thuộc quyền sửa, tiêu chí nghiệm thu.
Nếu bất kỳ thông tin nào xung đột với prompt, ưu tiên CONTRACT.md đã được nhóm phê duyệt và báo xung đột; không tự đổi API/kiến trúc.
Không sửa ngoài phạm vi file được giao; không force push; không bịa kết quả test.
Sau đó thực hiện prompt nhiệm vụ dành cho ROLE, tạo commit thật và báo đúng các phần đã làm/chưa làm.
```

### Cách kiểm tra kết nối thành công

Trong terminal của Antigravity (lệnh chỉ đọc):

```powershell
git remote -v
git status
git branch --show-current
git log -1 --oneline
```

- `remote -v` cho thấy repo GitHub đúng.
- `status` cho thấy đang ở trong repository và có file chưa commit hay không.
- `branch --show-current` cho thấy branch đang dùng.
- `log -1 --oneline` cho thấy commit gần nhất đã có trong thư mục local.

Các lệnh trên **chưa đủ để xác nhận quyền push**. Quyền push chỉ được xác nhận khi đăng nhập hợp lệ và lệnh push thành công (hoặc khi UI thông báo thành công từ GitHub). Không cần chạy một push giả lên `main` để thử.

### Cách làm chính xác nhất cho buổi học đầu tiên

1. A tạo repo trên GitHub.
2. A clone repo bằng Antigravity, dán **Prompt A**, hoàn thành bản nền và push `main`.
3. A gửi **URL repo + commit hash của base + branch name + prompt B/C** cho hai thành viên.
4. B/C clone từ URL đó, xác nhận đúng `CONTRACT.md` và base commit, làm trên branch riêng.
5. Khi hoàn tất, B/C push hoặc xuất ZIP. A review rồi merge.
6. A chạy **Prompt kiểm tra tích hợp** ở mục 8.

**Phần quyết định chất lượng không phải “link GitHub” mà là: cùng code nền, cùng hợp đồng, giới hạn phạm vi sửa, review diff và kiểm thử thật.** GitHub là phương tiện lưu phiên bản, phối hợp và ghép code có kiểm soát.

**Lưu ý riêng về README:** Đây là file hướng dẫn nhóm đầy đủ. Nếu dùng file này làm `README.md` gốc trên repository, hãy báo cho người C để họ **cập nhật phần hướng dẫn sử dụng/báo cáo** thay vì ghi đè nội dung phân công và prompt của nhóm. Có thể giữ nguyên bản sao trong `docs/GROUP-GUIDE.md` nếu sau này muốn README gốc ngắn gọn hơn.

---

## 11. Nguồn tham khảo chính thức

- Google Antigravity — Getting Started / Projects: <https://antigravity.google/docs/getting-started>
- Google Antigravity — VCS & Terminal: <https://antigravity.google/blog/vcs-and-terminal/>
- Google Antigravity IDE — Overview: <https://antigravity.google/docs/ide/overview/>
- Google Antigravity — Agent Permissions: <https://antigravity.google/docs/settings?tab=ide>
- GitHub — Clone repository: <https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository>
- GitHub — Authentication: <https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github>
- GitHub — Upload files: <https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository>
- GitHub Pages — Publish from branch: <https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site>
- Baymard Institute — List and Filtering UX: <https://baymard.com/research-articles/current-state-product-list-and-filtering>
- Baymard Institute — Applied Filters: <https://baymard.com/research-articles/how-to-design-applied-filters>
- Nielsen Norman Group — 10 Usability Heuristics: <https://www.nngroup.com/articles/ten-usability-heuristics/>
- W3C — WCAG 2.2: <https://www.w3.org/TR/WCAG22/>
- Google — Core Web Vitals: <https://web.dev/articles/vitals>

*Tài liệu lập kế hoạch và prompt, không phải báo cáo hoàn thành thực nghiệm. Link, repo name và lệnh chứa USERNAME là ví dụ, phải thay bằng tài khoản thực tế.*
