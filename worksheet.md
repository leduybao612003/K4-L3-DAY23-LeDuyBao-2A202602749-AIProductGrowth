# Worksheet — AI Agent Gateway

Họ tên: Lê Duy Bảo · MSSV: 2A202602749 · Ngày làm: 09/10/2026

## Trạm 1 — Loại mô hình

**Câu chốt loại:** Chúng tôi là B2B vì tiền đến từ ngân sách vận hành hạ tầng AI của doanh nghiệp khách, người dùng thật là đội kỹ sư và quản lý hạ tầng AI của chính doanh nghiệp đó, và chúng tôi chỉ chạm họ qua việc đổi base_url trong Anthropic SDK và Slack app cảnh báo ngân sách, không chạm người dùng cuối của khách.

**Bảng đèn §3 của loại mình** (ghi đủ mọi đèn trong bảng):

| Đèn | ✅ / 🔧 / ❌ | Số nằm ở đâu / cần gì để đo |
|---|---|---|
| Time to first value (TTFV) | 🔧 | Cần log ngày ký LOI hoặc hợp đồng và ngày có báo cáo shadow mode đầu tiên của từng khách |
| Chi phí triển khai ÷ ACV | 🔧 | Cần log giờ triển khai theo khách; ACV lấy từ hợp đồng đầu tiên |
| Ai gánh hoá đơn token | 🔧 | Mô hình giá Day22 chọn khách tự trả token cho Anthropic; cần ghi thành điều khoản hợp đồng |
| Sales cycle | 🔧 | Cần ghi ngày từng giai đoạn pipeline của mỗi design partner |
| NRR | ❌ | Chưa có khách trả tiền; cần doanh thu của cùng một khách trong 12 tháng |
| Containment rate | ✅ | Bộ eval của gateway cho kết quả xử lý đúng 95,3% |
| Chi phí AI mỗi task ÷ giá bán | 🔧 | Mô hình Day22 cho 28,2% (tab 1_Cost_Job và 2_Pricing); cần log token, retry, infra theo task để lấy số thật |
| Hard policy violation | 🔧 | Cần log quyết định định tuyến và hard policy của từng khách |
| Cost saving vs baseline | 🔧 | Cần shadow mode replay traffic thật của khách |
| Gross Margin | ❌ | Chưa có doanh thu thật; mô hình Day22 cho 71,8% |

## Trạm 2 — Thẻ đèn

**North Star:** Time to first value (TTFV) — hiện tại chưa đo — mục tiêu ≤ 30 ngày

| # | Tầng (L/O/G) | Đèn | Định nghĩa (đếm gì · **không** đếm gì) | Công thức | Nhịp · ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | L | Time to first value (TTFV) | Đếm: số ngày lịch từ ngày khách ký LOI hoặc hợp đồng đến ngày có báo cáo shadow mode đầu tiên cho thấy khoản tiết kiệm trên traffic thật của khách. Không đếm: traffic test nội bộ, ngày chờ khách cấp quyền truy cập log | Ngày có báo cáo shadow mode đầu tiên trừ ngày ký LOI hoặc hợp đồng | Hằng tuần · Lê Duy Bảo | Cost saving vs baseline |
| 2 | L | Chi phí AI mỗi task ÷ giá bán | Đếm: chi phí LLM router, retry, infra và QA nội bộ của các task hoàn tất trong tuần. Không đếm: token khách gọi model đích (khách trả trực tiếp cho Anthropic), overhead R&D và sales | Cost/Job ÷ giá bán mỗi task ($0,012) | Hằng ngày · Lê Duy Bảo | Gross Margin |
| 3 | O | Containment rate | Đếm: task được định tuyến xong đúng policy, đạt chất lượng tối thiểu, đúng latency, không cần quản trị viên can thiệp. Không đếm: task chuyển cho quản trị viên, task lỗi kỹ thuật, task test nội bộ | Số task hoàn tất ÷ số task vào | Hằng tuần · Lê Duy Bảo | Gross Margin |
| 4 | O | Hard policy violation | Đếm: số request được định tuyến tới model không đủ điều kiện theo hard policy của khách. Không đếm: request bị chặn đúng policy, request test nội bộ | Số request vi phạm hard policy trong cửa sổ 30 ngày | Hằng tuần · Lê Duy Bảo | NRR |
| 5 | O | Cost saving vs baseline | Đếm: phần trăm chênh lệch giữa chi phí token baseline của khách (replay cùng traffic, mọi request về model mặc định hiện tại) và chi phí token sau định tuyến, trên traffic thật. Không đếm: tiết kiệm do nhà cung cấp đổi bảng giá, phí gateway | (Chi phí baseline trừ chi phí sau định tuyến) ÷ chi phí baseline | Hằng tuần · Lê Duy Bảo | NRR |
| 6 | G | Gross Margin | Đếm: (doanh thu usage trừ COGS gồm LLM router, retry, infra, QA nội bộ) của tháng. Không đếm: R&D, sales, doanh thu gói onboarding một lần | (Doanh thu usage trừ COGS) ÷ doanh thu usage | Hằng tháng · Lê Duy Bảo | Đèn kết quả của đèn 2 và đèn 3 |

Đèn chi phí AI là đèn số: 2

## Trạm 3 — Ngưỡng

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn [BM]/[MH]/[TB] | Lý do (1 câu) · ngày kiểm tra nếu [BM] |
|---|---|---|---|---|---|---|
| 1 | Time to first value (TTFV) | ≤ 30 ngày | 31 đến 45 ngày | > 45 ngày | [MH] | Shadow mode theo kế hoạch kéo dài 4 tuần tức 28 ngày, làm tròn lên 30; mức đỏ bằng 1,5 lần mốc 30 (Phụ lục [MH] 4) |
| 2 | Chi phí AI mỗi task ÷ giá bán | ≤ 33,3% | 33,4% đến 40% | > 40% | [MH] | Giá bán ≥ 3 lần Cost/Job tương ứng tỷ lệ ≤ 33,3%, Gross Margin tối thiểu 60% tương ứng ≤ 40% (Phụ lục [MH] 2) |
| 3 | Containment rate | ≥ 95% | 67,1% đến dưới 95% | < 67,1% | [MH] | 67,1% là containment tối thiểu để Gross Margin đạt 60% ở giá $0,012 (Phụ lục [MH] 1); 95% là mức eligible route rate đặt trong PRD của gateway |
| 4 | Hard policy violation | 0 vi phạm | 1 vi phạm trong 30 ngày | ≥ 2 vi phạm trong 30 ngày | [TB] | PRD của gateway đặt hard policy violation rate 0% làm tiêu chí release; chưa có baseline, đo 2 chu kỳ 30 ngày từ 16/11/2026 rồi lấy làm baseline, dự kiến có số ngày 15/01/2027 |
| 5 | Cost saving vs baseline | ≥ 16% | 15,2% đến dưới 16% | < 15,2% | [MH] | 15,2% là mức tiết kiệm mà giá bán bằng đúng 25% khoản tiết kiệm (Phụ lục [MH] 3); 16% là giả định của mô hình Day22 |
| 6 | Gross Margin | ≥ 60% | 50% đến dưới 60% | < 50% | [BM] | Tài liệu Day22 đặt Gross Margin tối thiểu 60% và coi dưới 50% là vùng nguy hiểm, benchmark AI native 2026 khoảng 53% (ICONIQ 2026); số chốt ngày 26/08/2026 |

### Phụ lục [MH] — phép tính (≥2)

**[MH] 1 — Containment rate**

```
Đầu vào (từ mô hình tài chính / Cost/Job của tôi): LLM router $0,0010375 mỗi task (Haiku 5.5 $0,10 và $0,50 mỗi 1M token, 6 lượt, có cache) · retry 8% của LLM = $0,0000830 · infra $0,0012 · QA nội bộ 0,2% task × 3 phút ÷ 60 × $9 mỗi giờ = $0,0009 · giá bán $0,012 · Gross Margin mục tiêu 60%
Phép tính: biến phí mỗi task thử v = 0,0010375 + 0,0000830 + 0,0012 = 0,0023205; containment tối thiểu R = (0,0023205 + 0,0009) ÷ (0,012 × (1 trừ 0,6)) = 0,0032205 ÷ 0,0048 = 0,6709. Với Gross Margin 50%: 0,0032205 ÷ (0,012 × 0,5) = 0,5368
Kết quả → 🟢 ≥ 95% · 🟡 67,1% đến dưới 95% · 🔴 < 67,1%
```

**[MH] 2 — Chi phí AI mỗi task ÷ giá bán**

```
Đầu vào: Cost/Job $0,003379 (tab 1_Cost_Job, containment 95,3%) · giá bán $0,012 · giá bán tối thiểu 3 lần Cost/Job · Gross Margin tối thiểu 60%
Phép tính: giá bán ≥ 3 × Cost/Job nên Cost/Job ÷ giá ≤ 1 ÷ 3 = 33,3%; Gross Margin 60% nên Cost/Job ÷ giá ≤ 1 trừ 0,6 = 40%; hiện tại 0,003379 ÷ 0,012 = 28,2%
Kết quả → 🟢 ≤ 33,3% · 🟡 33,4% đến 40% · 🔴 > 40%
```

**[MH] 3 — Cost saving vs baseline**

```
Đầu vào: giá bán $0,012 mỗi task · 95.300 task hoàn tất mỗi tháng (100.000 task × containment 95,3%) · chi phí token baseline $30.000 mỗi tháng · giá bán tối đa 25% khoản tiết kiệm
Phép tính: doanh thu = 0,012 × 95.300 = $1.143,6; tiết kiệm tối thiểu = 1.143,6 ÷ 0,25 = $4.574,4; tỷ lệ tiết kiệm tối thiểu = 4.574,4 ÷ 30.000 = 15,2%; mô hình Day22 giả định $4.800 ÷ 30.000 = 16%
Kết quả → 🟢 ≥ 16% · 🟡 15,2% đến dưới 16% · 🔴 < 15,2%
```

**[MH] 4 — Time to first value (TTFV)**

```
Đầu vào: shadow mode theo kế hoạch 4 tuần
Phép tính: 4 × 7 = 28 ngày, làm tròn lên 30 ngày; mức đỏ = 1,5 × 30 = 45 ngày
Kết quả → 🟢 ≤ 30 ngày · 🟡 31 đến 45 ngày · 🔴 > 45 ngày
```

## Trạm 4 — 5 luật quyết định

Đánh dấu ⏹ cho luật dừng (cần ≥2).

1. ⏹ **NẾU** containment rate < 67,1% **TRONG** 2 tuần liên tiếp **VÀ** mỗi tuần ≥ 1.000 task vào **THÌ** dừng nâng tỷ lệ canary và đóng băng việc ký khách mới 3 tuần, Lê Duy Bảo đưa nhóm task bị chuyển cho quản trị viên vào replay suite để sửa ngay trong tuần đó **KHÔNG THÌ** không được tăng giá bán trên $0,012 để bù Gross Margin.
2. ⏹ **NẾU** chi phí AI mỗi task ÷ giá bán > 40% **TRONG** 2 tuần liên tiếp **VÀ** mỗi tuần ≥ 5.000 task hoàn tất **THÌ** dừng gọi LLM classifier ở các lượt sau lượt đầu của cùng một task và dùng lại quyết định định tuyến đã lưu cho các lượt còn lại, Lê Duy Bảo hoàn thành trong 1 tuần **KHÔNG THÌ** không được chuyển router lên Sonnet 5.5 để tăng độ chính xác khi chưa tính lại Cost/Job.
3. ⏹ **NẾU** TTFV > 45 ngày **TRÊN** 2 khách gần nhất **THÌ** dừng nhận design partner mới và đưa Lê Duy Bảo trực tiếp làm cấu hình tại 2 khách đó trong 2 tuần **KHÔNG THÌ** không được giảm giá dưới $0,012 để kéo khách ký nhanh hơn.
4. ⏹ **NẾU** số hard policy violation ≥ 2 **TRONG** 30 ngày **VÀ** cùng một khách **THÌ** dừng route tự động cho khách đó, chuyển 100% task về model mặc định của khách ngay trong ngày phát hiện, Lê Duy Bảo viết thêm test hard policy và chạy lại replay **KHÔNG THÌ** không được bật lại route khi replay chưa đạt 0 vi phạm.
5. **NẾU** cost saving vs baseline < 15,2% **TRÊN** shadow mode 4 tuần **VÀ** ≥ 10.000 task đã replay **THÌ** đàm phán lại giá với khách đó về mức không quá 25% khoản tiết kiệm đo được, Lê Duy Bảo gửi báo cáo replay và đề xuất giá trong 1 tuần **KHÔNG THÌ** không được ký hợp đồng ở giá $0,012 và không được dùng con số 16% của mô hình để thuyết phục khách.
