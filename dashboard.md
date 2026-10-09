# OPERATING DASHBOARD — AI agent xử lý khiếu nại cho Green Car

**Loại mô hình:** B2B — Green Car trả tiền; đội CSKH/vận hành Green Car dùng agent. · **Cập nhật:** 09/10/2026 · Nguyễn Văn Thăng – 2A202602835  
**NORTH STAR:** **TTFV** — chưa có baseline — mục tiêu `<30 ngày/pilot`: ngày từ ký/go-live đến khi một khiếu nại thật được xử lý có ích và được Green Car xác nhận. *Các số tiền là giả định nháp, cần thay bằng mô hình tài chính thật.*

### Đèn báo sớm (Leading — nhìn hằng tuần)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---|---|---|---|
| TTFV | Chưa có baseline | `<30 ngày` / `30–60` / `>60` | [TB] rà soát sau 2 pilot (23/10/2026) | Usage depth → NRR; POC → paid |
| Xử lý đạt chuẩn ngay lần đầu | Chưa có baseline | `≥85%` / `70–<85%` / `<70%` | [TB] baseline sau 2 tuần, mẫu ≥30 ticket/tuần (23/10/2026) | Tự động hóa → GM; usage depth |

### Đèn vận hành (Operating — nhìn hằng tuần/tháng)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---|---|---|---|
| Usage depth | Chưa có baseline | `≥60%` / `30–<60%` / `<30%` | [TB] rà soát sau 2 tuần (23/10/2026) | NRR và mở rộng hợp đồng |
| Tỷ lệ tự động hóa xử lý | Chưa có baseline | `≥70%` / `40–<70%` / `<40%` | [TB] baseline sau 2 tuần, mẫu ≥30 ticket/tuần (23/10/2026) | Cost/Job → GM; POC → paid |
| Cost/Job ÷ giá thu/việc | `2.000đ / 5.000đ` (giả định) | `≤1.750đ` / `>1.750–2.250đ` / `>2.250đ` | [MH] ACV 180tr, 36.000 việc/năm, GM 55% | Gross Margin |
| Chi phí triển khai ÷ ACV | Chưa có baseline | `<15%` / `15–30%` / `>30%` | [MH] ACV 180tr; xanh <27tr, đỏ >54tr | Gross Margin và scale |

### Đèn kết quả (Lagging — nhìn hằng tháng/quý)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn |
|---|---|---|---|
| Gross Margin | Chưa có baseline | `≥55%` / `45–<55%` / `<45%` | [BM] AI-native 45% (2025), 53% (2026E); kiểm tra 09/10/2026 |
| NRR | Chưa có baseline | `≥110%` / `100–<110%` / `<100%` | [BM] trung vị SaaS NRR 101%; kiểm tra 09/10/2026 |

### 5 luật quyết định (⏹ = luật dừng)

1. ⏹ **NẾU** TTFV `>60 ngày` **TRÊN** 3 pilot/khách gần nhất, **THÌ** cắt pilot xuống một loại khiếu nại và một đội CSKH đến khi TTFV `<30 ngày`. **KHÔNG THÌ** không nhận pilot rộng hơn hoặc tuyển thêm sales.
2. ⏹ **NẾU** xử lý đạt chuẩn ngay lần đầu `<70%` **TRONG** 2 tuần, **VÀ** mỗi tuần QA ≥30 khiếu nại thật, **THÌ** dừng phản hồi tự động, chuyển sang nhân viên duyệt trước và sửa 3 nhóm lỗi lớn nhất. **KHÔNG THÌ** không mở rộng agent sang loại khiếu nại mới.
3. ⏹ **NẾU** Cost/Job `>50%` giá thu/việc **TRONG** 2 tuần, **VÀ** có ≥50 việc đạt chuẩn/tuần, **THÌ** giới hạn token/việc, tối ưu model/prompt và chuyển case vượt ngân sách sang nhân viên. **KHÔNG THÌ** không bật tự động hóa không giám sát cho case chi phí cao.
4. ⏹ **NẾU** chi phí triển khai `>30% ACV` **TRÊN** 3 khách/pilot, **THÌ** đóng băng yêu cầu tuỳ biến và chuẩn hoá template, checklist, connector. **KHÔNG THÌ** không ký khách mới cùng phạm vi và mức giá đó.
5. **NẾU** usage depth `<30%` **SAU** 60 ngày go-live, **THÌ** Customer Success tổ chức adoption trong 5 ngày và bắt buộc dùng agent cho một workflow trong 2 tuần. **KHÔNG THÌ** không bán thêm module/seat.

### Cổng gác 90 ngày

| Ngày | Metric (1) | Ngưỡng qua cổng | Bằng chứng | Nếu trượt |
|---|---|---|---|---|
| 30 | Nhân sự CSKH hoàn tất pilot có QA | `≥3` nhân sự xử lý `≥10` khiếu nại thật/người | Export log ticket + rubric QA v1 | **FIX:** sửa một workflow trong 30 ngày |
| 60 | TTFV | `<30 ngày` trên `≥2` pilot/workflow | Bảng ngày go-live và ngày giá trị đầu tiên | **PIVOT:** đổi phân khúc khiếu nại/value metric nếu đã FIX mà vẫn trượt |
| 90 | Xử lý đạt chuẩn ngay lần đầu | `≥70%` trên mẫu `≥100` khiếu nại thật | Pilot Report: log, rubric QA, kết quả mẫu | **KILL:** nếu đã FIX mà vẫn dưới ngưỡng |

**KILL CRITERIA:** Dừng hẳn hướng AI agent xử lý khiếu nại cho Green Car nếu đến **ngày 90**, sau một lần FIX, tỷ lệ xử lý đạt chuẩn ngay lần đầu vẫn **<70% trên ít nhất 100 khiếu nại thật**.

**CHƯA ĐO ĐƯỢC:** Chưa có baseline cho TTFV, QA lần đầu, usage depth, tự động hóa, triển khai, GM và NRR. Cần log ticket gắn mã agent/test/thật và trạng thái nhân viên chấp nhận; rubric QA; usage API/token theo ticket; danh sách seat; timesheet triển khai; ACV/hợp đồng và sổ doanh thu. Có số đầu tiên sau 2 tuần pilot (23/10/2026); NRR sau một chu kỳ gia hạn.
