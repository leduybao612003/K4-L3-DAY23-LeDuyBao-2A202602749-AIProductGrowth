# OPERATING DASHBOARD — AI Agent Gateway

**Loại mô hình:** B2B · **Cập nhật:** 09/10/2026 · Lê Duy Bảo – 2A202602749
**NORTH STAR:** Time to first value (TTFV) — hiện tại chưa đo — mục tiêu ≤ 30 ngày

### Đèn báo sớm (Leading — nhìn hằng ngày/tuần)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---|---|---|---|
| Time to first value (TTFV): số ngày từ ngày ký đến báo cáo shadow mode đầu tiên có số tiết kiệm | Chưa đo | 🟢 ≤ 30 ngày · 🟡 31 đến 45 · 🔴 > 45 | [MH] 4 tuần shadow mode = 28 ngày, làm tròn 30 | Cost saving vs baseline |
| Chi phí AI mỗi task ÷ giá bán | 28,2% 🟢 (mô hình Day22) | 🟢 ≤ 33,3% · 🟡 33,4% đến 40% · 🔴 > 40% | [MH] giá ≥ 3 lần Cost/Job; Gross Margin ≥ 60% | Gross Margin |

### Đèn vận hành (Operating — nhìn hằng tuần/tháng)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---|---|---|---|
| Containment rate | 95,3% 🟢 (bộ eval của gateway) | 🟢 ≥ 95% · 🟡 67,1% đến dưới 95% · 🔴 < 67,1% | [MH] containment tối thiểu để Gross Margin đạt 60% | Gross Margin |
| Hard policy violation (số vi phạm trong 30 ngày) | Chưa đo | 🟢 0 · 🟡 1 · 🔴 ≥ 2 | [TB] PRD đặt 0%, baseline sau 2 chu kỳ, có số ngày 15/01/2027 | NRR |
| Cost saving vs baseline | Chưa đo | 🟢 ≥ 16% · 🟡 15,2% đến dưới 16% · 🔴 < 15,2% | [MH] giá bán bằng 25% khoản tiết kiệm | NRR |

### Đèn kết quả (Lagging — nhìn hằng quý)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn |
|---|---|---|---|
| Gross Margin | 71,8% 🟢 (mô hình Day22, chưa có doanh thu thật) | 🟢 ≥ 60% · 🟡 50% đến dưới 60% · 🔴 < 50% | [BM] tài liệu Day22 và ICONIQ 2026, số chốt ngày 26/08/2026 |

### 5 luật quyết định (⏹ = luật dừng)

1. ⏹ NẾU containment rate < 67,1% TRONG 2 tuần liên tiếp VÀ mỗi tuần ≥ 1.000 task vào THÌ dừng nâng tỷ lệ canary và đóng băng việc ký khách mới 3 tuần, Lê Duy Bảo đưa nhóm task bị chuyển cho quản trị viên vào replay suite để sửa ngay trong tuần đó KHÔNG THÌ không được tăng giá bán trên $0,012 để bù Gross Margin.
2. ⏹ NẾU chi phí AI mỗi task ÷ giá bán > 40% TRONG 2 tuần liên tiếp VÀ mỗi tuần ≥ 5.000 task hoàn tất THÌ dừng gọi LLM classifier ở các lượt sau lượt đầu của cùng một task và dùng lại quyết định định tuyến đã lưu cho các lượt còn lại, Lê Duy Bảo hoàn thành trong 1 tuần KHÔNG THÌ không được chuyển router lên Sonnet 5.5 để tăng độ chính xác khi chưa tính lại Cost/Job.
3. ⏹ NẾU TTFV > 45 ngày TRÊN 2 khách gần nhất THÌ dừng nhận design partner mới và đưa Lê Duy Bảo trực tiếp làm cấu hình tại 2 khách đó trong 2 tuần KHÔNG THÌ không được giảm giá dưới $0,012 để kéo khách ký nhanh hơn.
4. ⏹ NẾU số hard policy violation ≥ 2 TRONG 30 ngày VÀ cùng một khách THÌ dừng route tự động cho khách đó, chuyển 100% task về model mặc định của khách ngay trong ngày phát hiện, Lê Duy Bảo viết thêm test hard policy và chạy lại replay KHÔNG THÌ không được bật lại route khi replay chưa đạt 0 vi phạm.
5. NẾU cost saving vs baseline < 15,2% TRÊN shadow mode 4 tuần VÀ ≥ 10.000 task đã replay THÌ đàm phán lại giá với khách đó về mức không quá 25% khoản tiết kiệm đo được, Lê Duy Bảo gửi báo cáo replay và đề xuất giá trong 1 tuần KHÔNG THÌ không được ký hợp đồng ở giá $0,012 và không được dùng con số 16% của mô hình để thuyết phục khách.

### Cổng gác 90 ngày

| Ngày | Metric (1) | Ngưỡng qua cổng | Bằng chứng | Nếu trượt |
|---|---|---|---|---|
| 30 (08/11/2026) | Số design partner đã chốt định nghĩa Job và hard policy bằng văn bản | ≥ 5 khách | 5 file định nghĩa Job và hard policy, mỗi khách một file, đã được khách xác nhận | FIX một lần |
| 60 (08/12/2026) | TTFV | < 30 ngày trên ≥ 2 khách | 2 báo cáo shadow mode đầu tiên, mỗi báo cáo ghi ngày ký và ngày có số tiết kiệm | FIX một lần, nếu giả định gốc sai thì PIVOT |
| 90 (07/01/2027) | Cost saving vs baseline trên khách trả tiền | ≥ 15,2% ở cả 3 khách | Pilot Report 3 khách (hạn 05/01/2027) và log usage của 3 khách | FIX một lần, trượt tiếp thì KILL |

**KILL CRITERIA:** Dừng hẳn hướng này nếu đến 07/01/2027 chưa có khách nào trả tiền hoặc cost saving đo được dưới 15,2% ở mọi khách pilot sau một lần FIX đã dùng.

**CHƯA ĐO ĐƯỢC:** TTFV (cần: log ngày ký và ngày có báo cáo shadow mode đầu tiên của từng khách, khi nào có số: 23/11/2026); Cost saving vs baseline (cần: shadow mode replay traffic thật của khách, khi nào có số: 14/12/2026); Chi phí AI mỗi task ÷ giá bán thật (cần: log token, retry, infra theo task, khi nào có số: 23/11/2026); Hard policy violation (cần: log quyết định định tuyến và hard policy của khách, khi nào có số: 15/01/2027); Chi phí triển khai ÷ ACV (cần: log giờ triển khai theo khách và hợp đồng đầu tiên, khi nào có số: Tháng 2 đến 3 của kế hoạch 90 ngày); Sales cycle (cần: ngày từng giai đoạn pipeline của mỗi design partner, khi nào có số: 08/11/2026); Gross Margin thật và NRR (cần: khách trả tiền đầu tiên, khi nào có số: Gross Margin sau tháng doanh thu đầu tiên, NRR sau 12 tháng doanh thu của cùng một khách).
