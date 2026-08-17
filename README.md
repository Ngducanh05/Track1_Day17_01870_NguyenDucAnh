# Track 1 — Day 17 — Reverse-Engineering Solution Directive

## 1. Thông tin cá nhân và nhóm

| | |
|---|---|
| MHV | 2A202601870 |
| Họ và tên | Nguyễn Đức Anh |
| Tên nhóm | Anh Trai Mâm Hai |
| Case đã chọn | Case C — AI Support Radar |

**Thành viên nhóm:**

| Họ và tên | Mã học viên | Vai trò |
|---|---|---|
| Nguyễn Vũ Việt Anh | 2A202601742 | Đặt giả thuyết |
| Nguyễn Đình Quốc | 2A202601935 | Phỏng vấn |
| Mai Tiến Mạnh | 2A202601922 | Chuẩn bị câu hỏi |
| Nguyễn Đức Anh | 2A202601870 | Phỏng vấn |

---

## 2. Chặng 1 — Đặt giả thuyết (Problem Hypothesis Brief)

### 2.1 Solution — capability trung tính

Giúp giảng viên biết ai đang gặp khó và ở đâu — mà không cần tự quan sát hết từng học viên — để can thiệp đúng lúc.

> **Giả định đang ẩn:** "phân tích hành vi tự động + queue" là cách duy nhất để làm điều này. → Cần kiểm chứng trong quá trình điều tra.

### 2.2 Change (Output → Behavior → Outcome)

```
Support Queue (OUTPUT)
  → Instructor chủ động liên hệ đúng người đúng lúc (BEHAVIOR CHANGE)
    → Learner được hỗ trợ kịp thời (OUTCOME)
```

**Rủi ro lớn nhất:** nếu instructor không đổi hành vi (không xem / không liên hệ), chỉ có output, không có outcome.

### 2.3 Actor

| Actor | Pain có thể có |
|---|---|
| Instructor/Coach ← chọn điều tra trước | Không đủ thời gian rà soát tín hiệu từng học viên → phát hiện trễ/bỏ sót |
| Learner | Gặp khó nhưng không được phát hiện/hỗ trợ kịp thời |

**Lý do chọn Instructor trước:** họ là actor phải đổi hành vi để outcome xảy ra. Learner vẫn cần điều tra song song — để đối chiếu.

### 2.4 Situation & Job (JTBD)

> Khi tôi phụ trách nhiều học viên cùng lúc, tôi muốn biết sớm ai đang gặp khó và ở đâu, để can thiệp kịp thời trước khi họ rớt lại phía sau.

### 2.5 Pain — hai giả thuyết cạnh tranh

- **A (detection):** Instructor khó *nhận ra* ai gặp khó vì thiếu thời gian/công cụ rà soát → phát hiện trễ.
- **B (capacity):** Instructor *đã biết* ai gặp khó, nhưng không đủ thời gian/nguồn lực để can thiệp → bottleneck là hành động, không phải phát hiện.

→ Chọn điều tra **A trước**, vì đây là giả định lõi Support Queue đặt cược vào; cần loại trừ B sớm vì nếu B đúng, feature giải sai bài toán.

### 2.6 Evidence cần tìm

| Kiểm tra | Tin hơn nếu... | Nghi ngờ nếu... |
|---|---|---|
| Situation có thật | Lớp đông, không theo dõi hết được | Lớp nhỏ, dễ theo dõi hết |
| Pain có ý nghĩa | Có case cụ thể phát hiện trễ, hậu quả rõ | Luôn phát hiện kịp qua tương tác thường |
| Learner có phát tín hiệu | Learner mô tả rõ hành vi khi gặp khó (dừng lâu, đổi đáp án, hỏi AI Chat...) | Learner im lặng, không để lại dấu vết gì |

### 2.7 Problem Hypothesis (chốt) & điều bác bỏ

> Khi phụ trách nhiều học viên cùng lúc, instructor khó nhận ra kịp thời ai đang gặp khó và ở đâu vì thiếu công cụ/thời gian rà soát tín hiệu từng người → can thiệp trễ hoặc bỏ sót → học viên gặp khó âm thầm cho đến khi hậu quả xảy ra (rớt bài, bỏ học).

**Bác bỏ nếu:** lớp nhỏ (pain không tồn tại) / instructor biết nhưng không có capacity hành động (Pain B đúng) / learner không thực sự để lại tín hiệu quan sát được.

### 2.8 Parking Lot (5 hướng)

| Hướng | AI? |
|---|---|
| Support Queue tự động (bản gốc) | AI |
| Learner tự check-in định kỳ | Không AI |
| Buddy/coach theo dõi nhóm nhỏ cố định | Không AI |
| AI chỉ tổng hợp câu hỏi đã hỏi AI Chat (không suy đoán) | AI nhẹ |
| Dashboard số liệu thô, instructor tự nhìn | Không AI |

---

## 3. Chặng 2 — Conversation Guide (bản dùng cho phỏng vấn)

### Guide A — Lab Coach

**Tiêu chí tuyển:** Đã phụ trách giảng dạy/hỗ trợ một nhóm học viên online trong 30 ngày gần đây.

**Recruitment check:** "Hiện tại anh/chị có đang phụ trách giảng dạy hoặc hỗ trợ một nhóm học viên nào không? Khoảng bao nhiêu người?"

**Mở đầu:** "Tụi em đang tìm hiểu cách các giảng viên/coach theo dõi và hỗ trợ học viên trong quá trình học online — để hiểu công việc thực tế của anh/chị, không phải để giới thiệu hay xin ý kiến về sản phẩm nào cả."

**Story opener:** "Kể em nghe về lần gần nhất anh/chị nhận ra một học viên trong lớp/nhóm mình đang gặp khó khăn?"

| Big 3 | Câu hỏi |
|---|---|
| Detection (A) vs Capacity (B) | "Lúc đó anh/chị nhận ra bằng cách nào? Sau khi nhận ra, anh/chị đã làm gì tiếp theo?" |
| Quy mô / blind spot có thật | "Hiện anh/chị đang phụ trách khoảng bao nhiêu học viên? Có tương tác riêng thường xuyên với từng người không?" |
| Hậu quả phát hiện trễ | "Có lần nào anh/chị chỉ biết một học viên gặp khó khi đã quá muộn không — kể em nghe chuyện đó?" |

### Guide B — Learner

**Tiêu chí tuyển:** Đã học online và có lúc cảm thấy chưa hiểu/gặp khó trong 7 ngày gần đây.

**Recruitment check:** "Tuần vừa rồi bạn có học online không? Có lúc nào bạn cảm thấy bí, chưa hiểu một phần nào đó không?"

**Mở đầu:** "Mình đang tìm hiểu trải nghiệm học online thực tế của mọi người — không phải khảo sát ý kiến về tính năng nào, chỉ muốn nghe câu chuyện thật của bạn thôi."

**Story opener:** "Kể mình nghe về lần gần nhất bạn học một phần nào đó mà cảm thấy chưa hiểu hoặc bí?"

| Big 3 | Câu hỏi |
|---|---|
| Có để lại dấu vết hành vi hay im lặng bỏ qua | "Lúc đó bạn đã làm gì — dừng lại đọc lại, hỏi ai đó, bỏ qua luôn, hay làm gì khác?" |
| Workaround hiện tại | "Sau đó bạn xử lý phần khó đó như thế nào? Có ai giúp không, hay tự bạn tìm cách?" |
| Phản ứng khi được chủ động hỏi thăm | "Có bao giờ giảng viên, trợ giảng, hay bạn học chủ động hỏi thăm đúng lúc bạn đang gặp khó chưa? Lúc đó bạn cảm thấy thế nào?" |

**Probe bank:** "Chuyện gì xảy ra tiếp theo?" / "Bạn đã làm gì?" / "Vì sao chọn cách đó?" / "Phần nào khó nhất?" / "Đã thử cách khác chưa?" / "Hậu quả là gì?" / "Lần trước đó là khi nào?"

**Ba phản xạ:** Khen → *Deflect* (cảm ơn, quay lại hiện tại) · Câu chung chung/tương lai → *Anchor* ("lần gần nhất là khi nào?") · Feature request → *Dig* ("giúp làm được gì? hiện tại xử lý sao?")

### Checkpoint 2

- [x] Cả 2 guide neo vào sự kiện gần đây
- [x] Q1–Q3 nối thẳng Big 3
- [x] Không lộ solution (Support Queue / AI phân tích)

---

## 4. Chặng 3 — Interview Findings

### 4.1 Tổng quan

3 buổi phỏng vấn (`interview/recording 1–3.m4a`): **1 Learner (MSSV 01420)** + **2 Lab Coach (Dương, Mây)**. Cả 3 đều đạt tiêu chí tuyển.

### 4.2 Tóm tắt theo interviewee

| Interviewee | Vai trò | Câu chuyện / bối cảnh | Hành vi thực tế | Khó khăn / workaround | Hậu quả | Điều bất ngờ |
|---|---|---|---|---|---|---|
| MSSV 01420 | Learner | Là học viên, có khó khăn khi tiếp thu kiến thức | Đọc lại slide nhiều lần, giơ tay hỏi labcoach | Rụt rè, không dám giơ tay hỏi labcoach, hoặc bỏ qua kiến thức | Miss kiến thức, không follow theo bài học | Không có |
| Dương | Lab Coach | Quản lý khoảng 40–60 học viên | Đi quanh và hỏi về phần kiến thức (không chỉ hỏi "em làm xong chưa") | Nhiều học viên không nói ra vấn đề, đơn giản là "em làm xong rồi" | Miss kiến thức, học viên không follow theo bài học | Phần mềm V-learn session đã có tính năng *[ghi chú bị cắt — cần bổ sung]* |
| Mây | Lab Coach | Quản lý khoảng 40–60 học viên | *(Ghi chép trùng với Dương — cần xác nhận lại)* | Nhiều học viên không nói ra vấn đề | Miss kiến thức, học viên không follow theo bài học | Phần mềm V-learn session đã có tính năng *[ghi chú bị cắt — cần bổ sung]* |

### 4.3 Đối chiếu với Big 3 & giả thuyết

**Instructor (Dương & Mây)**
- **Detection (A) vs Capacity (B):** Cả hai coach *đang* chủ động đi quanh và hỏi sâu về kiến thức — tức họ có cách phát hiện thủ công và đang dùng nó. Bottleneck không nằm ở "thiếu công cụ rà soát" mà ở chỗ **học viên không để lộ vấn đề** ("em làm xong rồi"). → Nghiêng về Pain A, nhưng nguyên nhân là *tín hiệu learner bị ẩn*, không phải coach thiếu thời gian rà soát. Chưa có bằng chứng rõ cho Pain B.
- **Quy mô / blind spot có thật:** 40–60 học viên → không thể một mình theo dõi hết, situation có thật.
- **Hậu quả phát hiện trễ:** miss kiến thức, học viên không follow theo bài học — có hậu quả, nhưng ghi chú còn chung, chưa rõ case "đã quá muộn" cụ thể.

**Learner (MSSV 01420)**
- **Có để lại dấu vết hành vi?** Có tín hiệu quan sát được (*đọc lại slide nhiều lần, giơ tay hỏi*), nhưng đồng thời có lúc giấu đi (*rụt rè, không dám hỏi, bỏ qua kiến thức*). → Tín hiệu tồn tại nhưng **không nhất quán**; thời điểm "đọc lại slide nhiều lần" là cửa sổ để Support Queue bắt được trước khi learner bỏ qua.
- **Workaround hiện tại:** tự đọc lại slide, giơ tay hỏi labcoach.
- **Được chủ động hỏi thăm:** ghi chú chưa rõ, cần bổ sung.

**Tác động lên giả thuyết lõi**
- Pain A được hỗ trợ một phần: lớp đông + learner không tự nói → phát hiện trễ/bỏ sót là thật.
- Cần soi lại giả định "thiếu công cụ/thời gian": coach thực tế *đang* chủ động đi quanh; nếu họ chấp nhận cách này, value của "queue tự động" là giúp họ biết **sớm hơn và không bỏ sót**, chứ không phải "lần đầu có công cụ".

### 4.4 Điều bất ngờ / cần follow-up

1. **"Phần mềm V-learn session đã có tính năng..."** (cả 2 coach) — ghi chú bị cắt. Cần bổ sung: tính năng gì? Nó đang giải quyết Pain này chưa? Nếu đã có, giả định "không có công cụ tồn tại" bị bác bỏ / cần reposition.
2. **Ghi chép của Mây trùng hoàn toàn với Dương** — cần xác nhận lại, không dùng làm bằng chứng độc lập nếu chưa chắc chắn.
3. **Learner:** không ghi nhận bất ngờ/trái giả thuyết trong buổi phỏng vấn.

---

## 5. Practice Reflection

*Nội dung dưới đây là bản nháp nhóm rút ra khi rà soát bản ghi Chặng 3 — cần đối chiếu lại với buổi phỏng vấn thật trước khi nộp.*

1. **Câu hỏi nào của mình bị dẫn dắt, hoặc vô tình làm lộ solution?**
   Câu Big 3 thứ 3 của Guide B — "Có bao giờ giảng viên, trợ giảng, hay bạn học **chủ động hỏi thăm đúng lúc** bạn đang gặp khó chưa?" — vô tình gợi ý luôn hướng giải pháp (chủ động hỏi thăm, đúng lúc), và câu phụ "Lúc đó bạn cảm thấy thế nào?" kéo về cảm xúc chung chung thay vì hành vi cụ thể. Câu Recruitment check của Guide B ("Có lúc nào bạn cảm thấy **bí, chưa hiểu**...?") cũng hơi dẫn dắt vì nhồi sẵn từ khóa của giả thuyết.

2. **Câu hỏi nào không đào ra được hành vi cụ thể (chỉ ra ý kiến/mong muốn chung chung)?**
   Câu về hậu quả phát hiện trễ ở Guide A ("Có lần nào anh/chị chỉ biết một học viên gặp khó khi đã quá muộn không?") mới dừng ở "miss kiến thức, học viên không follow theo bài học" — khá chung, chưa có case cụ thể kèm mốc thời gian. Tương tự, câu "Sau đó bạn xử lý phần khó đó thế nào?" ở Guide B mới nhận được "đọc lại slide, giơ tay hỏi labcoach" nhưng chưa bám vào một tình huống rõ ràng (bài nào, phần nào, mất bao lâu).

3. **Nếu phỏng vấn lại, mình sẽ sửa gì trong cách hỏi hoặc thứ tự câu hỏi?**
   - Viết lại câu gợi ý solution của Guide B thành trung lập hơn, ví dụ "Có ai từng để ý và giúp đỡ bạn lúc bạn đang bí chưa?", và anchor theo sự kiện thay vì hỏi cảm xúc.
   - Với Guide A, thêm probe ép kể theo timeline: "Đó là bài học nào? Anh/chị nhận ra bằng cách nào? Nếu không nhận ra, chuyện gì đã xảy ra?" để lấy được case "đã quá muộn" cụ thể.
   - Khi coach nhắc "V-learn session đã có tính năng...", phải hỏi follow-up ngay (tính năng gì, dùng thế nào, có giúp được không) — lần này để sót nên ghi chú bị cắt.
   - Tách ghi chép riêng cho từng coach và đối chiếu chéo, tránh dữ liệu bị trùng lẫn như bản ghi Mây/Dương.

---

## 6. AI Support Log

**AI (Claude) đã hỗ trợ:**
- Đi qua chuỗi suy luận Solution → Change → Actor → Situation & Job → Pain → Evidence để nháp Problem Hypothesis cho Case C, bao gồm dựng hai giả thuyết pain cạnh tranh (A: detection vs B: capacity).
- Dựng khung Conversation Guide (recruitment check, opener, Big 3 questions, probe bank) bám theo Big 3 đã chốt ở Chặng 2, cho cả hai nhóm interviewee (instructor và learner).
- Rà soát câu hỏi để tránh làm lộ solution hoặc hỏi ý kiến/dự đoán tương lai.
- Rà soát `interview/notes.md` và hai bản tóm gọn Chặng 1–2 do nhóm cung cấp, tổng hợp thành README hoàn chỉnh (bổ sung mục Chặng 3 — Interview Findings và đối chiếu với Big 3).

**AI KHÔNG được dùng để:**
- Tạo interview data, bịa quote hay hành vi của người được phỏng vấn.
- Suy diễn chi tiết mà interviewee chưa từng nói.
- Thay nhóm ra quyết định — các bản nháp AI đề xuất (kể cả mục 5) phải được nhóm đối chiếu với buổi phỏng vấn thật trước khi nộp.

**Điểm nhóm đã tự sửa sau khi review AI output:**
- **Đổi actor điều tra trước từ Learner sang Instructor:** instructor là người phải đổi hành vi thì outcome mới xảy ra; learner để điều tra song song, đối chiếu.
- **Tách Pain thành hai giả thuyết cạnh tranh A (detection) vs B (capacity)** và chốt điều tra A trước để loại trừ sớm rủi ro "feature giải sai bài toán".
- **Bỏ ý định hỏi thẳng learner về các tín hiệu kiểu AI-analytics** (dừng lâu, đổi đáp án) vì dễ làm lộ solution; thay bằng câu hỏi hành vi thật ("lúc đó bạn đã làm gì...").
- **Sau khi rà soát bản ghi Chặng 3:** ghi nhận cần follow-up tính năng "V-learn session" và tách ghi chép giữa các coach — đã đưa vào mục 4.4 và 5.
