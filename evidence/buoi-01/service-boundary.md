# Service Boundary của nhóm

## 1. Thông tin nhóm

- Tên nhóm: 3B
- Lớp: CNTT 17-10
- Thành viên: [Đinh Mạnh Đà],[Nguyễn Thị Thu Vui], [Hà Thị Phương Thanh], [Đỗ Công Ngọc Sơn]
- Service nhóm phụ trách: kiểm tra môi trường và thu thập minh chứng buổi 1
- Sản phẩm tổng thể của lớp:Hệ thống thiết lập và kiểm tra môi trường lab cho học phần

## 2. Actor

Ai tương tác với hệ thống/service?
- Sinh viên: người dùng chính chạy script kiểm tra môi trường và tạo minh chứng.
- Giảng viên / hệ thống đánh giá tự động: kiểm tra kết quả nộp bài trên GitHub Classroom.
- Docker Engine: nền tảng cung cấp container và image.
- GitHub Classroom / GitHub: nơi lưu repo, nhận bài và trích xuất evidence.


## 3. System Boundary

Nhóm em xây phần nào?

Phần nhóm kiểm soát:

- Các script kiểm tra môi trường (`scripts/smoke_test.ps1`, `scripts/smoke_test.sh`).
- Các script thu thập minh chứng (`scripts/collect_session01_evidence.ps1`, `scripts/collect_session01_evidence.sh`).
- File cấu hình môi trường (`environment.yml`, `requirements.txt`).
- File evidence được sinh ra trong `evidence/buoi-01/`.

Phần nhóm chỉ tích hợp:

- - Docker và Docker Compose để chạy container.
- Node.js, Python/Miniconda để thực hiện kiểm tra phần mềm.
- Git/GitHub để đồng bộ repo và nộp bài.
- Docker Hub hoặc registry để tải image.

## 4. Service Boundary

Service của nhóm có trách nhiệm gì?
- Kiểm tra phiên bản Docker, Docker Compose, Node.js và Python.
- Kiểm tra khả năng chạy container Docker cơ bản (hello-world).
- Tải trước các Docker image cần thiết cho học phần.
- Chạy smoke test môi trường lab.
- Thu thập minh chứng đầu ra và lưu vào thư mục `evidence/buoi-01/`.
- Đảm bảo môi trường đã sẵn sàng cho các buổi học tiếp theo.
Service KHÔNG làm gì?
- Không triển khai ứng dụng nghiệp vụ hoặc backend cụ thể.
- Không lưu trữ dữ liệu người dùng lâu dài.
- Không thực hiện phân tích dữ liệu phức tạp hoặc xử lý business logic.
- Không thay thế CI/CD hoàn chỉnh hay dịch vụ hosting web.
## 5. Input / Output

### Input

- Yêu cầu từ người dùng: chạy script kiểm tra và thu thập evidence.
- Cấu hình môi trường: `environment.yml`, `requirements.txt`, script PowerShell/Bash.
- Môi trường hệ điều hành và Docker đã cài đặt.
- Kết nối tới Docker registry / Docker Hub để tải image.
### Output

- Báo cáo trạng thái kiểm tra môi trường.
- File kết quả smoke test.
- File evidence thu thập được trong `evidence/buoi-01/`.
- Log chi tiết quá trình thực hiện.
- Các bước đề xuất xử lý nếu phát hiện lỗi môi trường.

## 6. API dự kiến

| Method | Endpoint | Mục đích |
|---|---|---|
| GET | /health | Kiểm tra trạng thái cơ bản của service kiểm tra môi trường |
| POST | /check-environment | Khởi chạy kiểm tra môi trường và smoke test |
| POST | /collect-evidence | Thu thập minh chứng và tạo file trong `evidence/buoi-01/` |
| GET | /evidence | Lấy danh sách các minh chứng đã được tạo |


## 7. Phụ thuộc service khác

Service này gọi đến service nào?
Service này gọi đến service nào?

- Docker Engine: để tạo và chạy container.
- Docker Hub / registry: để tải image sẵn sàng.
- Hệ điều hành và môi trường Python/Node.js: để chạy các script kiểm tra.
- GitHub/GitHub Classroom: để đồng bộ repo và nộp evidence.
Service nào gọi đến service này?
- Sinh viên trực tiếp gọi qua terminal hoặc PowerShell/Bash.
- Hệ thống đánh giá tự động có thể gọi gián tiếp bằng cách kiểm tra kết quả trong repo.

## 8. Sơ đồ minh họa

Có thể vẽ bằng Mermaid, draw.io, Ludichart hoặc ảnh chụp sơ đồ.
https://lucid.app/lucidchart/bfd9b5ba-d6cc-4a8d-bba3-baef792060c5/edit?viewport_loc=-1717%2C-2394%2C9705%2C5318%2C0_0&invitationId=inv_c3a963eb-3721-430b-9690-3bd1c65b6481
```mermaid
flowchart LR
    User[Actor] --> Service[Service của nhóm]
    Service --> DB[(Database)]
    Service --> Other[Service khác]
