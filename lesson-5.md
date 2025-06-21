
## Buổi 4: Permissionless và ví dụ Pump.fun

### Mục tiêu buổi học

* Hiểu khái niệm **“permissionless”** trong blockchain/Web3: hệ thống mở không cần cấp phép – bất cứ ai cũng có thể tham gia sử dụng, xây dựng, đóng góp mà không bị chặn bởi cơ quan trung ương.
* Phân biệt **permissionless vs permissioned**: (ví dụ blockchain công khai như Ethereum vs blockchain do doanh nghiệp quản lý yêu cầu quyền truy cập).
* Thấy được **sức mạnh của permissionless** thông qua ví dụ **Pump.fun**: một nền tảng trên Solana cho phép **bất kỳ ai** tạo memecoin và giao dịch mà không cần lập trình hay xin phép. Hiểu cách Pump.fun vận hành ở mức căn bản.
* Thảo luận **ưu nhược điểm của môi trường permissionless**: tự do sáng tạo và tiếp cận vs rủi ro lừa đảo, rác, chất lượng không kiểm soát. Hiểu tại sao tinh thần “mở cửa tự do” này quan trọng để Web3 phát triển, nhưng cũng đòi hỏi người dùng nâng cao cảnh giác và trách nhiệm.

### Nội dung chính

* **Định nghĩa “permissionless”:** Trong ngữ cảnh blockchain, *permissionless* (không cần cấp phép) nghĩa là **mạng lưới mở mà bất cứ ai cũng có thể tham gia** mà không cần được ai phê duyệt. Ví dụ: **Ethereum, Bitcoin** là mạng công khai – bất kỳ ai có kết nối internet đều có thể tạo ví, gửi giao dịch, chạy node, viết smart contract... không ai cấm hay phải cấp quyền mới được làm. *“Permissionless blockchain hoàn toàn trái ngược với blockchain có cấp phép – không có hạn chế nào và sự tham gia không bị quản trị viên kiểm soát”*.
* **Ví dụ đối lập – permissioned:** Để rõ hơn, giải thích khái niệm blockchain permissioned (có cấp phép) ví dụ như một hệ thống blockchain nội bộ ngân hàng: chỉ những người được ngân hàng cho phép mới chạy node hoặc gửi giao dịch. Hệ thống đó tập trung hơn, phù hợp doanh nghiệp nhưng **thiếu tính mở**. Web3 chủ yếu nói về **permissionless blockchain công khai**, vì tinh thần cốt lõi là mở cho tất cả mọi người (tương tự Internet mở).
* **Lợi ích của permissionless:**

  * **Tự do sáng tạo:** Nhà phát triển ở bất cứ đâu có ý tưởng đều có thể triển khai dApp, phát hành token… *mà không cần xin phép ai*. Điều này tạo môi trường đổi mới sôi động giống như Internet thời kỳ đầu – ai cũng có thể làm website, dịch vụ mới.
  * **Tiếp cận không rào cản:** Người dùng chỉ cần một chiếc ví là dùng được ứng dụng phi tập trung, không cần đăng ký giấy tờ, KYC phức tạp (trừ khi dịch vụ tự nguyện yêu cầu). Điều này quan trọng cho **tính bao trùm**: ví dụ người không có giấy tờ ngân hàng vẫn có thể tiếp cận tài chính DeFi trên blockchain mở.
  * **Không ai kiểm duyệt/tắt dịch vụ:** Một dApp hay token trên mạng permissionless có thể bị thị trường bỏ rơi nếu kém, nhưng không ai có thể ép buộc đóng nó được (ngoại trừ toàn bộ mạng lưới đồng thuận). Điều này khuyến khích **đa dạng ý tưởng** kể cả “khùng điên” – có thể 9/10 ý tưởng thất bại hoặc lừa đảo, nhưng 1 ý tưởng thành công có thể là đột phá (vd: Uniswap ra đời từ một cá nhân, ban đầu không qua thẩm định của cơ quan nào).
* **Nhược điểm của permissionless:**

  * **Chất lượng không kiểm soát:** Vì ai cũng có thể tạo token/dApp, nên **tràn ngập dự án rác, lừa đảo**. Người dùng phải tự phân biệt thật giả, dễ bị scam nếu thiếu kiến thức. (Có thể nêu con số: Hơn 90% dự án trên các nền tảng mở như DEX hay pump.fun có thể là rác, tạo ra rồi vài tiếng sau dev bán tháo, rug pull – theo một số đánh giá cộng đồng).
  * **Tắc nghẽn và phí:** Quá nhiều người dùng = mạng tải cao (như CryptoKitties tắc mạng Ethereum). Cần cơ chế kỹ thuật nâng cấp liên tục (ví dụ Ethereum sharding, layer-2) để duy trì permissionless mà vẫn hiệu quả.
  * **Pháp lý & quản lý:** Môi trường không kiểm soát khiến nhà quản lý lo ngại (rửa tiền, lừa đảo). Đây là thách thức: làm sao cân bằng giữa tự do và bảo vệ người dùng.
* **Case study – Pump.fun (trên Solana):**

  * **Pump.fun là gì:** Một nền tảng **phi tập trung, không cần cấp phép** trên blockchain Solana, cho phép **bất kỳ ai** (kể cả người mới) tạo và phát hành token riêng chỉ với vài cú nhấp chuột và một khoản phí SOL nhỏ. Không cần biết lập trình hay viết smart contract phức tạp – Pump.fun đã lo sẵn. Người dùng chỉ cần nhập tên token, ký hiệu, hình ảnh, mô tả, nộp một ít SOL (\~0.02 SOL) là token mới được tạo ra ngay.
  * **Cơ chế hoạt động:** Thay vì mỗi người tự viết hợp đồng và cung cấp thanh khoản lên DEX, Pump.fun **đơn giản hóa**: nền tảng có sẵn một hợp đồng chung (hợp đồng của Pump.fun) và sử dụng **bonding curve AMM** tích hợp. Mỗi token tạo ra sẽ được giao dịch thông qua một pool tự động với đường cong giá: **giá tăng khi có người mua, giảm khi có người bán**. Người tạo token không cần làm gì thêm (không cần đưa lên sàn, không cần lo thanh khoản ban đầu nhiều) – nền tảng lo cơ chế đó luôn. Đây là ví dụ về **permissionless trong tạo token**: ai cũng có thể tạo coin mới dễ như tạo blog.
  * **Hiện tượng memecoin Pump.fun:** Pump.fun nổi lên cuối 2023 - 2024 khi trào lưu memecoin quay lại trên Solana. Hàng loạt coin vui nhộn (có tên nhái các trend, người nổi tiếng, meme internet) được tạo mỗi ngày. Nhiều coin giá tăng vọt rồi giảm thảm hại trong vài giờ (pump and dump). Tuy đa phần là coin “rác” không có giá trị nội tại, Pump.fun vẫn **thu hút người dùng** vì tính giải trí và cơ hội kiếm lời nhanh. (Ví dụ: token như \$PEPE có thể tăng x10 rồi về 0 trong một ngày). Điều này minh họa rõ ưu và nhược của permissionless: **ai cũng có thể sáng tạo** (tốt), nhưng cũng **dễ bị lợi dụng cho mục đích đầu cơ, lừa đảo**.
  * **Con số minh họa:** (Nếu có) Pump.fun kể từ ra mắt đã tạo ra hàng ngàn token và thu về doanh thu phí đáng kể vì số lượng người tham gia lớn. Alliance DAO (đơn vị đứng sau Pump.fun) báo cáo rằng chỉ trong vài tháng, nền tảng đã thu hàng trăm nghìn USD phí từ việc tạo token – chứng tỏ sức hút của mô hình permissionless này.
* **Bài học rút ra:**

  * Với người dùng: Permissionless trao quyền vào tay bạn, **nhưng cũng trao rủi ro**. Không có “ông bảo vệ” nào lọc dự án xấu giúp bạn. Vì vậy, trong Web3, người dùng cần biết tự bảo vệ (DYOR – Do Your Own Research).
  * Với hệ sinh thái: Môi trường mở thúc đẩy tốc độ thử nghiệm, sáng tạo phi thường (như “văn hóa khởi nghiệp” của Silicon Valley nhưng còn tự do hơn). Nhiều ý tưởng kỳ quặc có đất thử, và từ đó có thể lọt ra những viên ngọc quý.
  * **Tại sao quan trọng:** Nếu Web3 muốn **phổ biến toàn cầu** như Internet, tính permissionless là then chốt. Tưởng tượng nếu mỗi lần triển khai hợp đồng hay dApp phải xin phép cơ quan thì Web3 không khác gì hệ thống cũ. Chính sự mở cửa này phân biệt Web3 với các hệ thống tài chính/công nghệ trước đây.

### Cấu trúc buổi học

1. **Đặt vấn đề (5 phút):** Hỏi cả lớp: *“Nếu tôi muốn tạo ra đồng tiền số cho riêng mình, liệu tôi có làm được không? Có cần xin phép ai không?”*. Hãy để vài người đoán (đa phần sẽ ngạc nhiên khi biết “ai cũng tạo coin được”). Dẫn dắt: *“Blockchain cho phép điều đó vì tính permissionless – hôm nay ta khám phá khái niệm này.”*
2. **Trình bày khái niệm permissionless (10 phút):** Định nghĩa đơn giản + so sánh. Viết lên bảng hai cột: **Permissionless vs Permissioned**. Liệt kê vài đặc điểm đối lập (Mở vs Đóng, Ai cũng tham gia vs Chỉ người được mời, Không kiểm duyệt vs Kiểm soát bởi admin, Ẩn danh tham gia được vs Phải xác danh...). Giải thích tại sao Web3 chuộng permissionless (liên hệ triết lý tự do thông tin của Internet).
3. **Ví dụ minh họa chung (5 phút):** Lấy ví dụ một nền tảng quen thuộc: *“Đăng ứng dụng lên Google Play (cần tuân thủ quy định Google) vs triển khai smart contract lên Ethereum (bất kỳ ai triển khai, chỉ cần trả phí gas).”* Hoặc: *“Tạo token trên Ethereum: không ai cấm bạn tạo, trong khi tạo cổ phiếu trên thị trường chứng khoán truyền thống cần xin phép cơ quan quản lý.”* Qua đó học viên nắm tính chất “không rào cản”.
4. **Giới thiệu Pump.fun (15 phút):** Bắt đầu bằng mô tả Pump.fun và bối cảnh memecoin. Nếu có điều kiện demo: mở trang pump.fun trên trình duyệt, cho lớp xem giao diện (thường pump.fun hiển thị các token đang giao dịch, ví dụ danh sách coin, giá...). **Không thực sự tạo token nếu không có sẵn ví Solana test**, nhưng có thể dùng hình ảnh minh họa. Giảng viên giải thích quy trình tạo token: *chọn tên, biểu tượng, upload ảnh, trả một ít phí -> xong, token lên sàn ngay*. Có thể chuẩn bị **slide ảnh** để mô tả các bước.
5. **Phân tích ưu/nhược (10 phút):** Cùng lớp thảo luận quan sát từ ví dụ Pump.fun:

   * Hỏi: *“Điều hay ho của Pump.fun là gì?”* – Học viên có thể đáp: dễ dùng, ai cũng làm coin được, vui.
   * Hỏi: *“Nguy cơ là gì?”* – Đáp: lừa đảo, coin rác, người lạ có thể mất tiền nếu mua nhầm.
   * Giảng viên chốt lại bằng cách nhấn mạnh: **Quyền tự do càng cao thì trách nhiệm cá nhân càng lớn**.
6. **Mở rộng (5 phút):** Đề cập ngắn các ví dụ khác của permissionless: Uniswap (bất kỳ token ERC20 nào cũng có thể được list giao dịch trên DEX, không ai cấm) – sẽ học kỹ buổi 5. Hay Gitcoin/Grants trong Web3: ai cũng có thể xin tài trợ dự án mà cộng đồng thấy hay sẽ góp, không cần chờ quỹ đầu tư duyệt. Những điều này không đi sâu nhưng nhằm cho học viên thấy permissionless là chủ đạo ở nhiều mặt Web3.
7. **Thảo luận (10 phút):** Dùng câu hỏi gợi ý bên dưới để học viên suy nghĩ *tại sao* permissionless quan trọng, và liệu có giới hạn nào. Cuộc thảo luận có thể sôi nổi vì sẽ có người thấy “mở thế dễ loạn, cần quản lý”. Giảng viên nên trung lập, nhấn mạnh cả hai mặt.
8. **Kết thúc (5 phút):** Kết luận: Web3 cho phép *“mọi người trở thành người sáng tạo, người đóng góp”* dễ dàng hơn bao giờ hết – đó là sức mạnh của permissionless. Tuy nhiên, môi trường này cũng như “miền Tây hoang dã” – nhiều rủi ro, nên cần công cụ hỗ trợ (ví dụ: cộng đồng đánh giá uy tín, audit code). Liên hệ buổi sau: *“Nhắc đến permissionless, một ví dụ khác là Uniswap – nơi ai cũng có thể giao dịch token không cần qua sàn tập trung. Buổi sau chúng ta sẽ tìm hiểu về Uniswap và các sàn phi tập trung.”*

### Tài nguyên giảng dạy

* **Bài viết khái niệm:** *“Khái niệm trustless và permissionless trên blockchain là gì?”* (Fiahub Blog) – giải thích chi tiết hai thuật ngữ, phần permissionless có định nghĩa và so sánh rõ ràng.
* **Bài viết tham khảo:** *“Pumpfun (PUMP) là gì – Trình tạo Memecoin Solana”* (MEXC Blog 5/2025) – cung cấp thông tin cập nhật về Pump.fun, cách hoạt động và bối cảnh memecoin Solana.
* **Bài báo phân tích:** *“Pump.fun là gì? Hướng dẫn tạo meme bằng pump.fun”* (Coin68, 11/2024) – bài viết tiếng Việt hướng dẫn sử dụng Pump.fun và đánh giá hiện tượng memecoin, có số liệu về doanh thu, người dùng.
* **Website:** **pump.fun** – giao diện web trực quan. Nên kiểm tra trước buổi học, đề phòng trang web có nội dung nhạy cảm (vì cộng đồng memecoin đôi khi đăng hình phản cảm). Pump.fun có mục hiển thị token, hãy chọn ví dụ token phù hợp (tránh tên thô tục) để trình bày.
* **Cộng đồng thảo luận:** Tham khảo một số thảo luận trên Reddit (ví dụ r/solana) về Pump.fun để nắm bắt quan điểm cộng đồng, có thể trích một bình luận hay về ưu/nhược của trào lưu này, chia sẻ trong lớp.

### Hướng dẫn giảng dạy

* **Nhấn mạnh tính triết lý:** Permissionless thực ra là một **triết lý** nền tảng của Web3 (tương tự open-source trong phần mềm). Giảng viên có thể truyền tải nhiệt huyết: *“Chúng ta đang chứng kiến một môi trường công nghệ mà bất kỳ ai cũng có cơ hội đóng góp, sáng tạo mà không bị rào cản – đó là điều chưa từng có trước đây!”* Sự phấn khích này giúp học viên cảm nhận được tầm quan trọng, thay vì chỉ thấy đó là thuật ngữ kỹ thuật.
* **Đồng thời cảnh báo thực tế:** Song song, cần thực tế: dẫn chứng các **mặt trái** cụ thể để học viên không lầm tưởng mọi thứ “màu hồng”. Ví dụ: kể một tình huống *scam* đơn giản như “Alice thấy token X mới nổi, mua vào Pump.fun, 5 phút sau dev rút thanh khoản, Alice mất sạch tiền”. Từ đó khuyên họ bài học *“do your own research”*.
* **Tương tác qua câu hỏi:** Hãy hỏi học viên những câu như: *“Bạn có ý tưởng ứng dụng hay token gì muốn tạo không? Giờ bạn biết mình có thể tự làm mà không cần gọi vốn hay xin phép!”*. Biết đâu một bạn developer sẽ nảy ra sáng kiến. Mục tiêu là khuyến khích tư duy rằng *ai cũng có thể trở thành người sáng tạo trong Web3*, giảm mặc cảm “công nghệ cao siêu”.
* **Sử dụng phép so sánh:** So sánh permissionless blockchain với **Internet mở**: bất kỳ ai cũng có thể tạo website, blog mà không cơ quan nào cấp phép – điều này dẫn đến bùng nổ nội dung (tốt có, xấu có) trên Internet. Tương tự, Web3 sẽ bùng nổ dịch vụ tài chính, game, nội dung do người dùng tự tạo. Hỏi: *“Nếu thuở đầu Internet mà bị kiểm duyệt chặt, liệu có Google, Facebook hôm nay? Web3 cũng vậy, cần môi trường thoáng để có ‘Google của Web3’ trong tương lai.”*
* **Chuẩn bị các phản biện:** Một số học viên có thể lo ngại: *“Không quản lý thì lừa đảo đầy rẫy, nguy hiểm quá.”* Hãy thừa nhận điều đó, và giải thích hiện ngành blockchain cũng đang phát triển giải pháp: ví dụ **hệ thống xác thực phi tập trung (decentralized reputation)**, audit code, cộng đồng cảnh báo nhau. Nói rõ: *permissionless không đồng nghĩa vô pháp, mà là trao quyền quản lý xuống cho cộng đồng thay vì cơ quan trung ương*.

### Câu hỏi thảo luận gợi ý

* **Tại sao một hệ sinh thái mở (permissionless) lại thúc đẩy đổi mới sáng tạo hơn?** – Học viên thảo luận: vì rào cản gia nhập thấp, nhiều người tham gia hơn => nhiều ý tưởng; cạnh tranh tự do buộc dự án phải nỗ lực hơn; ví như hệ điều hành open-source có nhiều ứng dụng sáng tạo. Giảng viên dẫn: *“Nhiều đầu thì hơn một đầu”*, môi trường mở tạo hiệu ứng “quần chúng cùng xây”.
* **Nhược điểm lớn nhất của hệ thống không cần cấp phép là gì?** – Dự kiến câu trả lời: lừa đảo nhiều, spam, khó kiểm soát nội dung xấu (như web mở có cả web đen). Giảng viên có thể chốt: cần phát triển cách **quản trị cộng đồng** và công nghệ lọc thông minh thay vì cổng kiểm duyệt tập trung.
* **Làm thế nào để người dùng bình thường tự bảo vệ mình trong thế giới permissionless?** – Học viên có thể đề xuất: tìm hiểu kỹ dự án trước khi tham gia (đọc whitepaper, kiểm tra code/audit, nghe ngóng cộng đồng), bắt đầu với số tiền nhỏ, sử dụng các dịch vụ bảo hiểm DeFi nếu có. Mục đích: nhấn mạnh vai trò **giáo dục và tự chịu trách nhiệm** của người dùng Web3.
* **Bạn đánh giá thế nào về việc ai cũng có thể tạo ra đồng token riêng dễ dàng?** – Gợi suy nghĩ về cả hai mặt: tích cực (dân chủ hóa việc huy động vốn, cá nhân hóa nền kinh tế – ví dụ influencer tạo token cho fan) và tiêu cực (loạn coin rác, lãng phí nguồn lực). Cuộc thảo luận này giúp học viên tự hình thành quan điểm và hiểu bức tranh toàn cảnh.
* **Theo bạn, có lĩnh vực nào *không nên* hoàn toàn permissionless không?** – Câu hỏi thú vị để học viên suy xét giới hạn. Ví dụ một số có thể nói: *“Y tế hay bầu cử có lẽ cần kiểm soát nhất định”*. Điều này mở ra khái niệm về **lai ghép**: có thể kết hợp blockchain mở với xác thực danh tính (như giải pháp quadratic funding có KYC). Giảng viên không cần đi sâu, chỉ ghi nhận ý kiến để học viên thấy không có một khuôn mẫu áp dụng cho mọi thứ, nhưng đa phần dịch vụ Web3 hướng tới permissionless tối đa có thể.

---
