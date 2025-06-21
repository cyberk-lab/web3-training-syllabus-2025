# Uniswap và các sàn phi tập trung (DEX) 

**Đối tượng học viên:** Designer, Lập trình viên và QA engineer *chưa có nền tảng về Web3*, đã học qua Bitcoin và Ethereum cơ bản.

**Mục tiêu buổi học:** Hiểu **DEX (Decentralized Exchange)** là gì và khác gì so với sàn giao dịch tập trung (CEX) truyền thống. Nắm được **cách Uniswap hoạt động** ở mức cơ bản: khái niệm **AMM (Automated Market Maker)**, **liquidity pool** (bể thanh khoản), **liquidity provider** (người cung cấp thanh khoản), và cơ chế định giá tự động (công thức x*y=k). Biết được **lợi ích của DEX**: giao dịch không cần trung gian, ai cũng có thể niêm yết token (permissionless listing), người dùng giữ quyền kiểm soát tài sản trong suốt quá trình. Thảo luận **tại sao DEX quan trọng trong Web3**: DEX hiện thực hóa tài chính phi tập trung (DeFi), giúp hoàn thiện hệ sinh thái không cần ngân hàng hay sàn tập trung, đồng thời tạo nền tảng cho nhiều ứng dụng tài chính sáng tạo (yield farming, lending, v.v.).

---

## 1. Dẫn nhập (20 phút)

### 1.1. Khởi động & Câu hỏi mở
Giảng viên mở đầu bằng câu hỏi gợi mở: *"Ai ở đây từng mua Bitcoin/ETH trên sàn như Binance chưa? Trải nghiệm thế nào?"*. Để vài người chia sẻ (đăng ký, chờ KYC, nộp tiền...). Sau đó hỏi: *"Có cách nào trade crypto **không cần sàn** không?"*. 

**Liên hệ thực tế:** Hỏi tiếp về những bất tiện khi sử dụng sàn tập trung: phải tin tưởng sàn giữ tiền, lo sợ sàn bị hack hay phá sản, chờ đợi KYC phức tạp, chỉ trade được những coin sàn cho phép. Từ đó, giảng viên dẫn dắt: *"Sẽ thế nào nếu chúng ta có thể giao dịch crypto trực tiếp từ ví của mình, không cần gửi tiền cho ai?"* – giới thiệu ý tưởng về sàn giao dịch phi tập trung.

### 1.2. Câu chuyện dẫn dắt
Giảng viên kể câu chuyện về **Hayden Adams** – người sáng lập Uniswap: *"Năm 2017, một chàng trai trẻ tên Hayden Adams vừa bị sa thải khỏi công việc kỹ sư cơ khí. Thất nghiệp và không biết làm gì, anh bắt đầu học lập trình Solidity theo một bài blog của Vitalik Buterin về 'Automated Market Makers'. Từ một ý tưởng đơn giản - tạo ra một cách để mọi người có thể trao đổi token mà không cần sàn giao dịch truyền thống - Hayden đã xây dựng nên Uniswap."*

**Nhấn mạnh:** *"Điều đặc biệt là Hayden không phải chuyên gia tài chính hay có background về trading. Anh chỉ là một người bình thường với một ý tưởng: tại sao chúng ta lại phải tin tưởng và phụ thuộc vào các sàn giao dịch tập trung? Từ ý tưởng đó, Uniswap đã ra đời và thay đổi cách chúng ta nghĩ về giao dịch trong thế giới crypto."*

### 1.3. Ví dụ hấp dẫn
Giảng viên chia sẻ một con số gây ấn tượng: *"Các bạn có đoán được khối lượng giao dịch hàng ngày của Uniswap là bao nhiêu không?"* (Cho học viên vài giây suy nghĩ). *"Có thời điểm năm 2021, khối lượng giao dịch 24h của Uniswap còn **vượt cả Coinbase** - một trong những sàn crypto lớn nhất thế giới! Từ một dự án của một cá nhân thất nghiệp, Uniswap đã trở thành một trong những nền tảng giao dịch quan trọng nhất trong DeFi."*

**Câu hỏi kích thích:** *"Điều gì khiến một sàn 'không có chủ' lại có thể cạnh tranh và thậm chí vượt qua các sàn truyền thống được quản lý bởi các công ty lớn?"*

### 1.4. Giới thiệu chủ đề
Từ những dẫn dắt trên, giảng viên chính thức giới thiệu chủ đề buổi học: *"Hôm nay chúng ta sẽ cùng tìm hiểu về Uniswap và thế giới của các sàn giao dịch phi tập trung (DEX). Chúng ta sẽ khám phá cách chúng hoạt động, tại sao chúng lại quan trọng, và làm thế nào chúng đang định hình lại tương lai của tài chính. Tất cả sẽ được giải thích một cách đơn giản nhất, không đòi hỏi các bạn có kiến thức chuyên sâu về tài chính hay lập trình."*

---

## 2. Định nghĩa & Giải thích (20 phút)

Giảng viên trình bày các khái niệm chính một cách dễ hiểu, kèm ví dụ/so sánh trực quan:

**DEX (Decentralized Exchange - Sàn giao dịch phi tập trung):** DEX là nền tảng cho phép người dùng giao dịch tiền mã hóa trực tiếp với nhau **mà không cần trung gian**. Khác với sàn tập trung (CEX), người dùng không cần tạo tài khoản hay gửi tiền vào sàn - họ giao dịch trực tiếp từ ví cá nhân thông qua smart contract. Uniswap là DEX hàng đầu trên Ethereum, cho phép hoán đổi các token ERC-20 một cách tự động và không cần cấp phép.

**CEX vs DEX (So sánh):** *CEX (Centralized Exchange)* như Binance, Coinbase yêu cầu người dùng tạo tài khoản, nạp tiền vào ví sàn (tài sản do sàn giữ hộ), giao dịch qua sổ lệnh khớp lệnh mua-bán. Ưu điểm: tốc độ nhanh, giao diện thân thiện, có hỗ trợ khách hàng. Nhược điểm: tập trung nên có rủi ro bị hack, sàn phá sản, phải tin tưởng sàn, chỉ niêm yết các coin đã qua kiểm duyệt. *DEX* ngược lại: người dùng giao dịch từ ví cá nhân qua smart contract, không cần tin cậy bên thứ ba, không cần KYC, mọi token tuân thủ chuẩn đều có thể giao dịch (permissionless listing). Rủi ro: người dùng tự quản lý tài sản, giao dịch có thể chậm và phí cao khi mạng tắc.

**AMM (Automated Market Maker - Tạo lập thị trường tự động):** Thay vì sử dụng sổ lệnh truyền thống, Uniswap dùng AMM - một cơ chế tự động tạo ra giá và thanh khoản. Hệ thống này hoạt động thông qua các **bể thanh khoản (liquidity pools)** chứa cặp token. Ví dụ: pool ETH/USDT chứa một lượng ETH và USDT. Khi ai đó muốn mua ETH, họ nạp USDT vào pool và rút ETH ra, giá ETH sẽ tự động tăng theo thuật toán.

**Liquidity Pool (Bể thanh khoản):** Đây là "kho chứa" các cặp token được người dùng gửi vào để tạo thanh khoản cho việc giao dịch. Ví dụ pool ETH/USDT có thể chứa 100 ETH và 200,000 USDT. Mọi giao dịch hoán đổi đều diễn ra thông qua pool này - người mua ETH sẽ nạp USDT vào và rút ETH ra, làm thay đổi tỷ lệ trong pool và do đó thay đổi giá.

**Công thức x*y=k:** Uniswap V2 sử dụng công thức này để đảm bảo **sản phẩm không đổi**. Nếu pool có X token A và Y token B, thì X * Y phải luôn bằng hằng số k. Khi có giao dịch làm thay đổi X hoặc Y, giá sẽ tự động điều chỉnh để duy trì công thức này. *Ví dụ đơn giản:* Pool có 100 ETH và 200,000 USDT (k = 20,000,000). Khi ai đó mua 1 ETH, pool còn 99 ETH, để giữ k không đổi, pool phải có ~202,020 USDT - nghĩa là người mua phải trả ~2,020 USDT cho 1 ETH.

**Liquidity Provider (LP - Người cung cấp thanh khoản):** Đây là những người gửi tài sản vào các pool để tạo thanh khoản. LP phải gửi **cả hai token** theo tỷ lệ hiện tại của pool và nhận về **LP token** đại diện cho phần đóng góp của họ. Đổi lại, LP được hưởng **phí giao dịch** (Uniswap V2 thu 0.3% mỗi giao dịch) chia theo tỷ lệ đóng góp. Tuy nhiên, LP cũng chịu rủi ro **impermanent loss** khi giá token biến động mạnh.

**Slippage (Trượt giá):** Khi giao dịch khối lượng lớn so với kích thước pool, giá sẽ thay đổi đáng kể giữa lúc đặt lệnh và lúc thực hiện. Ví dụ: muốn mua 10 ETH từ pool nhỏ có thể khiến giá ETH tăng từ 2000 USDT lên 2100 USDT trong cùng giao dịch đó.

---

## 3. Ứng dụng & Mở rộng (15 phút)

### 3.1. Vai trò & Trường hợp sử dụng thực tế
**Vai trò hiện tại của DEX:** DEX đã trở thành xương sống của hệ sinh thái DeFi, tạo ra một **thị trường tài chính mở 24/7** không biên giới. Uniswap và các DEX khác cho phép giao dịch hàng nghìn token mà các sàn tập trung không niêm yết, đặc biệt là các token mới hoặc của các dự án nhỏ. 

**Trường hợp sử dụng cụ thể:** Nhà đầu tư có thể swap token ngay lập tức mà không cần chờ KYC; các dự án startup có thể tạo thanh khoản cho token của mình mà không cần xin sàn lớn niêm yết; người dùng có thể trở thành LP để kiếm phí từ việc cung cấp thanh khoản. DEX cũng là nền tảng cho các chiến lược DeFi phức tạp như yield farming, arbitrage, và flash loans.

### 3.2. Ảnh hưởng đến các lĩnh vực liên quan
**Tác động đến tài chính truyền thống:** DEX thách thức mô hình trung gian truyền thống bằng cách chứng minh rằng thị trường có thể tự vận hành hiệu quả mà không cần market maker tập trung. Điều này buộc các sàn CEX phải cải thiện dịch vụ và giảm phí để cạnh tranh.

**Ảnh hưởng đến công việc học viên:** Đối với **developer**, hiểu DEX mở ra cơ hội phát triển các ứng dụng tài chính phi tập trung hoặc tích hợp chức năng swap vào dApp. **Designer** cần thiết kế UX cho các giao dịch phức tạp hơn (slippage, gas fee, LP) một cách thân thiện. **QA** cần hiểu các edge case đặc thù của DEX như front-running, MEV, impermanent loss để thiết kế test case phù hợp.

### 3.3. Ảnh hưởng đến tương lai (Web3)
**Nền tảng cho DeFi:** DEX là viên gạch đầu tiên của hệ sinh thái DeFi. Không có DEX, sẽ không có lending protocols (vì cần swap collateral), yield farming (cần swap rewards), hay stablecoin (cần arbitrage để duy trì peg). DEX tạo ra tính **composability** - khả năng các protocol khác xây dựng lên trên và tương tác với nhau.

**Tầm nhìn omnichain:** Tương lai, DEX sẽ phát triển thành các nền tảng giao dịch đa chuỗi, cho phép swap token giữa các blockchain khác nhau một cách liền mạch. Điều này sẽ tạo ra một thị trường tài chính toàn cầu thực sự, nơi mọi tài sản số đều có thể được giao dịch tự do.

**Dân chủ hóa tài chính:** DEX hiện thực hóa tầm nhìn về một hệ thống tài chính **permissionless** - nơi bất kỳ ai cũng có thể tham gia, tạo thị trường, và cung cấp dịch vụ tài chính mà không cần xin phép cơ quan quản lý hay tổ chức trung gian.

---

## 4. Thảo luận mở (10 phút)

Giảng viên đưa ra các câu hỏi để cả lớp cùng thảo luận, khuyến khích học viên chia sẻ suy nghĩ:

**1. So với giao dịch trên sàn Binance, giao dịch trên Uniswap khác những gì?**
*Gợi ý trả lời:* Học viên có thể liệt kê: không cần nạp tiền vào sàn, dùng ví cá nhân; không có lệnh mua/bán mà swap ngay; phải trả phí gas; chọn token tùy ý (nhiều lựa chọn hơn); không có customer support nếu có vấn đề. Câu này kiểm tra hiểu biết vừa học và giúp so sánh trực quan.

**2. Điều gì đảm bảo người dùng A có thể mua token từ người dùng B trên DEX mà không cần họ gặp nhau?**
*Gợi ý trả lời:* Gợi họ giải thích vai trò **pool thanh khoản**. Đáp án: vì đã có pool, người mua bán chỉ tương tác với pool chứ không cần khớp trực tiếp với nhau như sàn order book. Pool đóng vai trò như một "ngân hàng tự động" luôn sẵn sàng mua/bán.

**3. Ai là người định giá token trên Uniswap?**
*Gợi ý trả lời:* Học viên có thể lúng túng, giảng viên hướng: *"Có phải một tổ chức hay thuật toán AI định giá không?"* Đáp án: **công thức AMM** định giá dựa trên số lượng trong pool, tức là *chính người giao dịch gián tiếp quyết định giá* (mua nhiều thì giá tăng, bán nhiều giá giảm). Thị trường tự điều tiết.

**4. Bạn có nghĩ DEX sẽ thay thế hoàn toàn sàn tập trung không? Tại sao?**
*Gợi ý trả lời:* Câu hỏi mở để tranh luận. Có người sẽ nói có (vì triết lý phi tập trung), có người nói không (vì người mới vẫn cần giao diện thân thiện, CEX cung cấp fiat onramp). Giảng viên kết luận: có lẽ cả hai sẽ cùng tồn tại, phục vụ các nhu cầu khác nhau, nhưng DEX chắc chắn sẽ ngày càng quan trọng.

---

## 5. Tóm tắt (5 phút)

### 5.1. Tổng kết các ý chính
* **DEX vs CEX:** Sàn phi tập trung cho phép giao dịch trực tiếp từ ví cá nhân thông qua smart contract, không cần tin tưởng bên trung gian, nhưng đòi hỏi người dùng tự chịu trách nhiệm cao hơn.
* **Cơ chế AMM:** Uniswap sử dụng bể thanh khoản và công thức x*y=k để tự động tạo giá và thanh khoản, thay thế mô hình sổ lệnh truyền thống.
* **Vai trò của LP:** Người cung cấp thanh khoản kiếm phí từ giao dịch nhưng chịu rủi ro impermanent loss, tạo nên động lực kinh tế để duy trì hoạt động của DEX.
* **Tính permissionless:** Bất kỳ ai cũng có thể tạo pool, list token, hoặc tham gia giao dịch mà không cần xin phép, thể hiện tinh thần mở của Web3.

### 5.2. Nhấn mạnh thông điệp cốt lõi
**"DEX chứng minh rằng thị trường tài chính có thể tự vận hành hiệu quả mà không cần trung gian, mở ra một tương lai nơi mọi người đều có quyền bình đẳng tiếp cận và tham gia vào hệ thống tài chính toàn cầu."**

### 5.3. Cầu nối đến bài học tiếp theo
*"Chúng ta đã thấy cách DEX cho phép giao dịch các token có thể thay thế (fungible) như ETH, USDT một cách tự do. Nhưng Web3 còn mở ra khả năng sở hữu và giao dịch những tài sản số **độc nhất** - không thể thay thế. Buổi tới, chúng ta sẽ khám phá thế giới của NFT (Non-Fungible Token) và cách chúng đang tạo ra một nền kinh tế mới cho người sáng tạo."*

---

## 6. Tài liệu tham khảo thêm

**Video YouTube tham khảo:**
* **"Uniswap (UNI) là gì? Tìm hiểu về sàn DEX hàng đầu"** (Coin68) – Giải thích dễ hiểu về Uniswap và cơ chế AMM bằng tiếng Việt (~15 phút)
* **"Cách sử dụng Uniswap cho người mới"** – Video hướng dẫn thực hành swap token trên Uniswap (~10 phút)

**Bài viết tham khảo:**
* **"Mô hình hoạt động Uniswap V2 – Nền tảng của các AMM"** (Coin98 Insights) – Phân tích chi tiết công thức x*y=k và ví dụ số cụ thể
* **DefiLlama** – Trang web thống kê khối lượng giao dịch DEX và thị phần Uniswap realtime

**Case study:**
* **"Bài học từ sự kiện FTX sập năm 2022"** – Nghiên cứu về tầm quan trọng của việc tự giữ tài sản và sử dụng DEX thay vì tin tưởng sàn tập trung