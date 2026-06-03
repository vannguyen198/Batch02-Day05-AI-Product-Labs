# Workshop — Finding Note - NEO Vietnam Airlines Web

## 1. Sản phẩm

| Sản phẩm | AI feature | Cách truy cập |
|---|---|---|
| Vietnam Airlines — NEO | Chatbot hỗ trợ vé, hành lý, khiếu nại | Website/Zalo VNA |

## 2. Dùng thử: promise vs reality

Promise:

- Thuận tiện tra cứu, giải đáp nhanh chóng (24/7) mọi thắc mắc liên quan đến thông tin hành trình, mua vé, thanh toán và
nhiều tính năng khác
- User được hứa trợ giúp cho hành khách chuẩn bị đặt vé, mua vé, check-in,...
- Kỳ vọng: tra cứu, giải đáp được các thông tin chính thống, cụ thể về quy định, kiện hàng, thông tin chuyến bay, hành lý,...
- Điểm gãy xuất hiện: 

| # | Input thử | Phản ứng thực tế của NEO | Điểm gãy |
|---|---|---|---|
|1|Mình bay đi Hàn Quốc khởi hành từ Hà Nội thì có được mang 2 kiện hành lý ký gửi không|NEO bị bối rối vì câu hỏi kép. Nó sẽ chọn từ khóa "mạnh" hơn là "Mua thêm" hoặc "Hành lý" để trả ra một mớ định nghĩa dài dòng về quy định hành lý quá cước, nhưng bỏ quên vế "mua trên app như thế nào" và "có được giảm giá không"|User nhận được một khối văn bản quy định giá tiền, nhưng vẫn không biết thực hiện việc mua ra sao, cũng không rõ mức giá mình đang đọc đã được áp dụng giảm giá chưa|
|2|Chuyến bay VN123 ngày mai của mình bị đổi giờ, giờ mình muốn đổi sang chuyến khác miễn phí hoặc hoàn vé thì làm thế nào|NEO chỉ trả ra quy định chung về việc hoàn/đổi vé (Ví dụ: Vé hạng nào được đổi, phí đổi là bao nhiêu) theo dạng lý thuyết|Khách hàng đang trong tâm trạng hoang mang vì bị đổi giờ bay, nhưng chatbot không giải quyết được "End-to-end" (không có nút bấm chọn chuyến bay mới ngay tại chỗ). Khách hàng buộc phải thoát chat, tự vào lại website để tìm mục "Quản lý đặt chỗ" để tự thao tác lại|
|3|Hệ thống báo lỗi không cho mình check-in online, mình muốn gặp nhân viên tổng đài ngay" hoặc gõ liên tục "gặp nhân viên", "gặp người thật"|Câu trả lời mang tính chất "bỏ lửng". Hệ thống bắt người dùng chờ đợi vô định hướng, không rõ thời gian, màn hình chat đóng băng hoàn toàn|User bị kẹt ở trạng thái hoang mang không biết có nên tắt app/thoát màn hình chat hay không. Nếu thoát ra thì sợ mất lượt, nếu ở lại thì phải nhìn chằm chằm vào màn hình mà không biết khi nào mới được trả lời|

## 3. Vẽ 4 paths

| Path | Câu hỏi cần trả lời |Thực tế, đề xuất|
|---|---|---|
| Happy | Khi AI đúng và tự tin, user thấy gì? |User thấy khối thông tin chuẩn xác và phân loại rõ ràng. Cụ thể,khi hỏi về hành lý đi Hàn Quốc, NEO tự tin trả ra ngay chính xác định mức cân nặng cho 3 hạng vé (Thương gia, Phổ thông đặc biệt, Phổ thông). Văn bản hiển thị rõ ràng, xuống dòng dễ đọc|
| Low-confidence | Khi AI không chắc, hệ thống có hỏi lại, show options hoặc chuyển người không? |Hệ thống có show options nhưng chưa tối ưu (bỏ lửng). Khi user hỏi một câu chứa thông tin cá nhân hoặc bối cảnh động, NEO "không chắc" vé của user thuộc hạng nào nên đã đẩy ngược nhiệm vụ bắt user tự kiểm tra vé. Cần bổ sung ngay các nút bấm lựa chọn (Options Button) như: [Tra cứu mã đặt chỗ của tôi] hoặc [Nhập mã PNR 6 ký tự] để thu hẹp phạm vi bối cảnh.|
| Failure | Khi AI sai, user biết bằng cách nào và sửa thế nào? |User biết khi nhận được câu trả lời không liên quan hoặc hệ thống im lặng, cũng như sửa bằng cách yêu cầu Handoff. Khi gặp lỗi check-in trực tuyến (AI không thể xử lý sâu vào core hệ thống), user nhận ra AI thất bại vì nó trả lời vòng vo hoặc báo bận. User chủ động sửa sai bằng cách gõ: "Gặp nhân viên" để ép hệ thống chuyển đổi luồng.|
| Correction | Khi user sửa, correction có được lưu/log/học lại không hay biến mất? |Hiện tại biến mất (Trạng thái đóng băng). Đề xuất phải được Lưu/Log để học lại. Thực tế: Khi hệ thống báo "Vui lòng chờ một lát...", cuộc hội thoại rơi vào khoảng lặng vô định. Nếu user kiên nhẫn chờ hoặc gõ lại câu hỏi, dữ liệu sửa sai này dễ bị trôi mất khi tắt chat To-be: Hệ thống cần ghi nhận Correction log như lưu lại chính xác câu hỏi bị lỗi khiến user phải đòi gặp người thật, chuyển toàn bộ log này cho nhân viên nhân sự đọc tiếp quản (để user không phải gõ lại), đồng thời gắn tag lỗi để AI học lại (retrain) sau này.|

## 4. Viết finding thành quyết định
Quyết định 1:
Khi user hỏi "Hành trình từ Hà Nội đi Hàn Quốc được mang bao nhiêu kiện hành lý?",
AI trả lời đúng quy định chung nhưng bỏ lửng bối cảnh cá nhân và bắt user tự đi lục vé,
hậu quả là user bị kẹt, phải thoát màn hình chat để tìm hạng vé trong email/PDF rồi tự đối chiếu.
Lỗi thuộc layer UX Recovery + Data-tool.
Nên sửa bằng UX/Fallback: Thêm low-confidence path hiển thị ngay 2 nút bấm "Kiểm tra vé của tôi" (nếu đã đăng nhập app) hoặc "Nhập mã đặt chỗ PNR" để hệ thống tự động quét hạng vé và trả ra câu trả lời đích danh.

Quyết định 2:
Khi user gõ "Muốn gặp nhân viên tổng đài ngay do lỗi check-in online",
AI xác nhận chuyển giao nhưng thả nổi trạng thái "vui lòng chờ một lát" mà không có chỉ báo thời gian,
hậu quả là user rơi vào trạng thái hoang mang vô định, không biết có nên giữ màn hình chat không và dễ dàng rời bỏ (drop-off).
Lỗi thuộc layer UX Recovery + Human role.
Nên sửa bằng UX + Fallback: Hiển thị thanh trạng thái hàng đợi thời gian thực (Ví dụ: "Bạn là người thứ 2 - Chờ 1p30s") kèm 2 nút bấm lựa chọn: "Tiếp tục chờ tại đây" hoặc "Nhận thông báo qua Zalo/SMS khi nhân viên vào" để user yên tâm thoát app.

## 5. Sketch as-is / to-be

| Luồng hiện tại (As-is) | Luồng cải tiến (To-be) |
| :--- | :--- |
| **1. Ý ĐỊNH USER (TRIGGER)**<br>User gõ câu hỏi: *"Hành lý đi Hàn Quốc được mang bao nhiêu kg?"* | **1. Ý ĐỊNH USER (TRIGGER)**<br>User gõ câu hỏi: *"Hành lý đi Hàn Quốc được mang bao nhiêu kg?"* |
| **2. AI XỬ LÝ (HAPPY PATH)**<br>AI tự tin trả ra block text phân loại quy định:<br>- Thương gia: 2 kiện 32kg<br>- Phổ thông: 1 kiện 23kg | **2. AI XỬ LÝ (HAPPY PATH)**<br>AI tự tin trả ra block text phân loại quy định:<br>- Thương gia: 2 kiện 32kg<br>- Phổ thông: 1 kiện 23kg |
| **3. ĐIỂM GÃY (LOW-CONFIDENCE PATH)**<br>AI không biết hạng vé cụ thể của user.<br>➔ **AI làm:** Bảo user tự đi check vé.<br>➔ **User:** Bị kẹt, phải thoát chat để tự mò lại thông tin vé của mình. | **3. SỬA ĐIỂM GÃY (LOW-CONFIDENCE PATH)**<br>AI không biết hạng vé cụ thể của user.<br>➔ **AI làm:** Gợi ý ngay **2 Options Buttons** dưới câu trả lời:<br>`[Tra cứu vé của tôi]` \| `[Nhập mã đặt chỗ 6 ký tự]`<br>➔ **User:** Click chọn nhanh để hệ thống tự quét và trả lời đích danh hạng vé của mình ngay tại chỗ. |
| **4. AI THẤT BẠI (FAILURE PATH)**<br>User thấy phức tạp, gõ sửa sai: *"Cho gặp nhân viên trực tiếp!"*<br>➔ **AI làm:** Trả lời *"Vui lòng chờ một lát..."* rồi im lặng.<br>➔ **User:** Bị kẹt vì không biết chờ đến bao giờ, màn hình không có chỉ báo trạng thái. | **4. KHẮC PHỤC SAI LẦM (UX RECOVERY PATH)**<br>User muốn đổi luồng, gõ: *"Cho gặp nhân viên!"*<br>➔ **AI làm (Handoff thông minh):** Kích hoạt hệ thống hàng đợi thời gian thực:<br>💬 *“Bạn là người thứ 2 trong hàng đợi. Dự kiến chờ: 1p30s.”*<br>Kèm **2 Fallback Buttons**:<br>`[Tiếp tục chờ tại đây]` \| `[Nhận tin nhắn báo qua Zalo khi có người trực]` |
| **5. HẬU QUẢ (IMPACT)**<br>User bỏ cuộc (Drop-off), tràn qua gọi hotline làm nghẽn tổng đài thoại. | **5. KẾT QUẢ (VALUE)**<br>User làm chủ thời gian, hoàn thành tương tác **End-to-end** trong một màn hình chat duy nhất. |
## 6. Tự kiểm trước khi nộp

- [x] Có ít nhất 1 screenshot hoặc observation cụ thể.
- [x] Có đủ 4 paths hoặc nói rõ path nào chưa có trong product.
- [x] Finding được viết thành product decision, không chỉ là nhận xét.
- [x] Sketch có as-is và to-be.
- [x] Có một câu nói rõ finding này sẽ đổi gì trong SPEC.
