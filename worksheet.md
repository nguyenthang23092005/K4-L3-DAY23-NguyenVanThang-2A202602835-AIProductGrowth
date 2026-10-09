# Worksheet — AI agent hỗ trợ xử lý khiếu nại cho Green Car

Họ tên: Nguyễn Văn Thắng · MSSV: 2A202602835 · Ngày làm: 09/10/2026

## Số liệu đầu vào

| Chỉ số | Giá trị | Đơn vị / ghi chú |
|---|---:|---|
| ARPU | 15.000.000 | VND/Green Car/tháng = ACV 180.000.000 VND/năm |
| Gross margin | 55% | mục tiêu sau direct COGS |
| CAC | 36.000.000 | VND/khách hàng B2B |
| CAC payback mục tiêu | 6 | tháng |
| Runway | 9 | tháng |
| Value Metric | 1 khiếu nại đạt chuẩn | bản xử lý đạt rubric QA |
| Cost/Job | 2.000 | VND/khiếu nại đạt chuẩn; giả định 3.000 khiếu nại/tháng |

## Trạm 1 — Loại mô hình

**Câu chốt loại:** Chúng tôi là **B2B** vì Green Car là doanh nghiệp trả tiền và đội CSKH/vận hành của Green Car trực tiếp dùng AI agent để xử lý khiếu nại; khách đi xe chỉ là nguồn phát sinh khiếu nại, không trực tiếp dùng hay trả tiền cho sản phẩm.

**Bảng đèn §3 của loại mình** (ghi đủ mọi đèn trong bảng):

| Đèn | ✅ / 🔧 / ❌ | Số nằm ở đâu / cần gì để đo |
|---|---|---|
| Time-to-first-value (TTFV) ⭐ | 🔧 | Cần ghi nhận ngày ký/go-live và ngày đầu tiên đội Green Car xử lý được một khiếu nại có kết quả đo được qua agent; lấy từ hợp đồng, CRM và log agent. |
| Pipeline coverage | 🔧 | Cần CRM có giá trị các cơ hội đã đủ điều kiện và target doanh thu theo quý. |
| % deal chết ở khâu security/procurement | 🔧 | Cần trường “lý do closed-lost” bắt buộc trong CRM, phân loại riêng security/procurement. |
| POC → paid | 🔧 | Cần danh sách POC/pilot cùng trạng thái chuyển đổi sang hợp đồng trả tiền; đối soát với hợp đồng hoặc hóa đơn. |
| Sales cycle (tuần) | 🔧 | Cần ngày cơ hội đủ điều kiện và ngày ký hợp đồng cho từng deal trong CRM. |
| Usage depth trong tài khoản | 🔧 | Cần số seat/nhân sự CSKH được cấp quyền và số người thực sự dùng agent ít nhất 1 lần mỗi tuần từ log đăng nhập và log xử lý. |
| Chi phí triển khai ÷ ACV | 🔧 | Cần timesheet triển khai, đơn giá giờ công, chi phí tích hợp và ACV trong hợp đồng Green Car. |
| Tập trung doanh thu | 🔧 | Cần doanh thu theo khách hàng mỗi tháng từ hóa đơn/kế toán. Khi chỉ có Green Car, metric sẽ là 100% và phải ghi rõ rủi ro phụ thuộc một khách. |
| NRR | 🔧 | Cần MRR/ARR đầu kỳ, doanh thu mở rộng/thu hẹp/churn theo cohort khách hàng; chỉ đo được sau ít nhất một chu kỳ gia hạn. |
| Gross Margin | 🔧 | Cần doanh thu Green Car trừ chi phí suy luận AI/token, hạ tầng, hỗ trợ trực tiếp và chi phí vận hành dịch vụ. |
| CAC payback | 🔧 | Cần CAC thực tế, ARPU/ACV và gross margin; lấy từ mô hình tài chính sau khi đã chốt hợp đồng. |

## Trạm 2 — Thẻ đèn

**North Star:** **Time-to-first-value (TTFV)** — hiện tại: chưa có baseline — mục tiêu: <30 ngày cho mỗi pilot Green Car. Giá trị đầu tiên là một khiếu nại thật được agent hỗ trợ xử lý, có kết quả được người phụ trách Green Car xác nhận; không phải chỉ cài đặt hoặc chạy demo.

| # | Tầng (L/O/G) | Đèn | Định nghĩa (đếm gì · **không** đếm gì) | Công thức | Nhịp · ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | L | Time-to-first-value (TTFV) | Số ngày từ ngày Green Car ký/go-live pilot đến ngày đầu tiên một khiếu nại thật được agent hỗ trợ xử lý và người phụ trách xác nhận kết quả có ích. **Không** tính dữ liệu demo, ticket test nội bộ hoặc chỉ hoàn tất cài đặt. | `ngày xác nhận giá trị đầu tiên − ngày ký/go-live` | Mỗi khách/pilot · Product lead lấy từ hợp đồng, log ticket và biên bản xác nhận | Usage depth → NRR; đồng thời báo trước POC → paid |
| 2 | L | Tỷ lệ xử lý đạt chuẩn ngay lần đầu | % khiếu nại thật mà agent tạo được bản phân loại, đề xuất hướng xử lý và nội dung phản hồi đạt rubric QA ngay lượt kiểm tra đầu tiên. **Không** tính ticket test, ticket thiếu dữ liệu đầu vào, hoặc ticket do nhân viên tự soạn hoàn toàn không dùng đề xuất agent. | `số khiếu nại đạt rubric QA ngay lần đầu ÷ số khiếu nại thật được QA` | Hằng tuần · QA lead lấy mẫu ngẫu nhiên từ log agent và chấm rubric | Tỷ lệ tự động hóa xử lý → Gross Margin và usage depth |
| 3 | O | Usage depth trong Green Car | % nhân sự CSKH/vận hành đã được cấp quyền có dùng agent để xử lý ít nhất 1 khiếu nại thật trong tuần. **Không** tính đăng nhập, mở dashboard, hoặc ticket test. | `số người dùng agent cho ≥1 khiếu nại thật/tuần ÷ số người được cấp quyền` | Hằng tuần · Customer success lấy từ danh sách seat và log xử lý | NRR và khả năng mở rộng hợp đồng |
| 4 | O | Tỷ lệ tự động hóa xử lý khiếu nại | % khiếu nại thật agent tạo bản phân loại và phản hồi/next step được nhân viên chấp nhận với chỉnh sửa không đáng kể, theo rubric QA. **Không** coi là tự động hóa nếu nhân viên viết lại phần lớn nội dung hoặc ticket bị escalated vì lỗi agent. | `số khiếu nại được chấp nhận với chỉnh sửa không đáng kể ÷ tổng khiếu nại thật được agent xử lý` | Hằng tuần · Ops/QA lead lấy từ trạng thái ticket và mẫu QA | Cost/Job → Gross Margin; đồng thời chứng minh giá trị để POC → paid |
| 5 | O | Chi phí AI trên một khiếu nại đạt chuẩn (Cost/Job) | Tổng chi phí model/inference trực tiếp của các phiên xử lý kết thúc bằng một khiếu nại đạt rubric QA. **Không** gộp chi phí nhân sự, sales hay ticket test; không chia trên mọi lượt prompt. | `tổng chi phí inference của các khiếu nại đạt chuẩn ÷ số khiếu nại đạt chuẩn` | Hằng tuần · Engineering/Finance lấy từ usage API và log ticket | Gross Margin; cảnh báo sớm khi chi phí token tăng | 
| 6 | O | Chi phí triển khai ÷ ACV | Tỷ lệ chi phí để đưa agent vào vận hành cho Green Car (giờ công × đơn giá + tích hợp) so với giá trị hợp đồng năm. **Không** gồm chi phí R&D dùng chung hay chi phí bán hàng. | `(giờ công triển khai × đơn giá + chi phí tích hợp trực tiếp) ÷ ACV` | Mỗi khách, rà soát hằng tháng · Project lead/Finance lấy từ timesheet, hóa đơn và hợp đồng | Gross Margin và khả năng scale triển khai |
| 7 | G | Gross Margin | Phần doanh thu Green Car còn lại sau chi phí trực tiếp để cung cấp dịch vụ: inference/token, hạ tầng trực tiếp, hỗ trợ trực tiếp và triển khai được phân bổ. **Không** trừ chi phí R&D, sales/marketing hoặc chi phí quản trị chung. | `(doanh thu − COGS trực tiếp) ÷ doanh thu` | Hằng tháng/quý · Finance đối soát hợp đồng, usage API và sổ chi phí | Bảng điểm cho Cost/Job, tự động hóa và chi phí triển khai |
| 8 | G | NRR | Tỷ lệ doanh thu định kỳ từ Green Car/cohort khách hàng đầu kỳ còn lại sau mở rộng, thu hẹp và churn. **Không** gồm doanh thu từ khách hoàn toàn mới trong kỳ. | `(ARR đầu kỳ + expansion − contraction − churn) ÷ ARR đầu kỳ` | Hằng quý · Finance/Customer success lấy từ hợp đồng và hóa đơn | Bảng điểm cho TTFV và usage depth |

Đèn chi phí AI là đèn số: **5 — Chi phí AI trên một khiếu nại đạt chuẩn (Cost/Job)**.

## Trạm 3 — Ngưỡng

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn [BM]/[MH]/[TB] | Lý do (1 câu) · ngày kiểm tra nếu [BM] |
|---|---|---|---|---|---|---|
| 1 | TTFV | <30 ngày | 30–60 ngày | >60 ngày | [TB] | Chưa có chuẩn nội bộ; lấy mốc B2B của HANDBOOK làm giới hạn vận hành và rà soát sau 2 pilot vào 23/10/2026. |
| 2 | Xử lý đạt chuẩn ngay lần đầu | ≥85% | 70–<85% | <70% | [TB] | Chưa có baseline; đo hai tuần với mẫu ≥30 ticket thật/tuần, sau đó thay bằng baseline nội bộ vào 23/10/2026. |
| 3 | Usage depth | ≥60% | 30–<60% | <30% | [TB] | Dùng mốc B2B trong HANDBOOK làm điểm xuất phát; xác nhận lại sau 2 tuần log seat vào 23/10/2026. |
| 4 | Tỷ lệ tự động hóa xử lý | ≥70% | 40–<70% | <40% | [TB] | Chưa có hai chu kỳ dữ liệu; đo baseline trên ticket thật trong hai tuần và chốt lại ngày 23/10/2026. |
| 5 | Cost/Job | ≤1.750đ | >1.750–2.250đ | >2.250đ | [MH] | Giá thu giả định 5.000đ/việc và GM mục tiêu 55% cho phép direct cost tối đa 2.250đ/việc; vượt mức này làm GM thấp hơn mô hình. |
| 6 | Chi phí triển khai ÷ ACV | <15% (27 triệu) | 15–30% (27–54 triệu) | >30% (>54 triệu) | [MH] | Với ACV 180 triệu và direct COGS tối đa 81 triệu theo GM 55%, triển khai vượt 54 triệu làm contribution năm đầu chỉ còn tối đa 45 triệu trước CAC. |
| 7 | Gross Margin | ≥55% | 45–<55% | <45% | [BM] | Mốc HANDBOOK: AI-native 45% năm 2025 và 53% năm 2026E; đặt 55% cao hơn dự báo ngành; kiểm tra 09/10/2026. |
| 8 | NRR | ≥110% | 100–<110% | <100% | [BM] | HANDBOOK nêu trung vị SaaS NRR 101%; 110% là mức tăng trưởng trong tài khoản; kiểm tra 09/10/2026. |

### Phụ lục [MH] — phép tính (≥2)

**[MH] 1 — Cost/Job**

```
Đầu vào (từ mô hình tài chính / Cost/Job của tôi): ACV = 180.000.000đ/năm; volume = 3.000 khiếu nại/tháng × 12 = 36.000 việc/năm; GM mục tiêu = 55%.
Phép tính: Giá thu/việc = 180.000.000 ÷ 36.000 = 5.000đ. Direct cost tối đa/việc = 5.000 × (1 − 55%) = 2.250đ. Vùng xanh giữ buffer 500đ/việc: 2.250 − 500 = 1.750đ.
Kết quả → 🟢 Cost/Job ≤1.750đ · 🟡 >1.750–2.250đ · 🔴 >2.250đ.
```

**[MH] 2 — Chi phí triển khai ÷ ACV**

```
Đầu vào: ACV = 180.000.000đ/năm; GM mục tiêu = 55%; direct COGS tối đa = 180.000.000 × 45% = 81.000.000đ.
Phép tính: Contribution sau direct COGS = 180.000.000 − 81.000.000 = 99.000.000đ. Cap triển khai xanh = 15% ACV = 27.000.000đ; mức đỏ = 30% ACV = 54.000.000đ. Khi triển khai >54.000.000đ, contribution năm đầu còn <45.000.000đ trước CAC 36.000.000đ, quá mỏng để scale.
Kết quả → 🟢 <27.000.000đ (<15% ACV) · 🟡 27.000.000–54.000.000đ (15–30%) · 🔴 >54.000.000đ (>30%).
```

## Trạm 4 — 5 luật quyết định

Đánh dấu ⏹ cho luật dừng (cần ≥2).

> Các ngưỡng [MH] dưới đây dùng bộ giả định đã ghi ở đầu worksheet; thay bằng số mô hình tài chính thật nếu có trước khi gửi LMS.

1. ⏹ **NẾU** TTFV >60 ngày **TRÊN** 3 pilot/khách gần nhất, **THÌ** cắt phạm vi pilot của Green Car xuống một loại khiếu nại và một đội CSKH cho đến khi TTFV <30 ngày. **KHÔNG THÌ** không nhận pilot rộng hơn và không tuyển thêm sales để bơm thêm deal vào quy trình đang tắc.
2. ⏹ **NẾU** tỷ lệ xử lý đạt chuẩn ngay lần đầu <70% **TRONG** 2 tuần liên tiếp, **VÀ** mỗi tuần có ít nhất 30 khiếu nại thật được QA, **THÌ** dừng gửi phản hồi tự động tới khách hàng, chuyển toàn bộ sang chế độ nhân viên duyệt trước khi gửi và sửa 3 nhóm lỗi QA xuất hiện nhiều nhất trong sprint kế tiếp. **KHÔNG THÌ** không mở rộng agent sang loại khiếu nại mới để bù volume.
3. ⏹ **NẾU** Cost/Job >50% doanh thu thu được trên một khiếu nại đạt chuẩn **TRONG** 2 tuần liên tiếp, **VÀ** có ít nhất 50 khiếu nại đạt chuẩn trong mỗi tuần, **THÌ** giới hạn ngân sách token cho mỗi khiếu nại, tối ưu prompt/model và chuyển các case vượt ngân sách sang hàng đợi nhân viên. **KHÔNG THÌ** không bật chế độ xử lý tự động không giám sát cho các case chi phí cao.
4. ⏹ **NẾU** chi phí triển khai >30% ACV **TRÊN** 3 khách/pilot liên tiếp, **THÌ** đóng băng nhận yêu cầu tuỳ biến mới, chuẩn hoá ba phần tốn công nhất thành template, checklist onboarding hoặc connector sẵn có. **KHÔNG THÌ** không ký khách mới với cùng phạm vi và mức giá hiện tại.
5. **NẾU** usage depth <30% **SAU** 60 ngày kể từ go-live Green Car, **THÌ** cử Customer Success cùng trưởng nhóm CSKH tổ chức một buổi adoption trong 5 ngày làm việc, chọn một workflow khiếu nại bắt buộc dùng agent trong 2 tuần và đo lại theo tuần. **KHÔNG THÌ** không chào bán thêm module hay mở rộng seat cho Green Car khi tài khoản chưa dùng hết phần đã mua.
