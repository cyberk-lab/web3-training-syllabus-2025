
## Buổi 3: Uniswap và các sàn phi tập trung (DEX)

### Mục tiêu buổi học

* Hiểu **DEX (Decentralized Exchange)** là gì và khác gì so với sàn giao dịch tập trung (CEX) truyền thống.
* Nắm được **cách Uniswap hoạt động** ở mức cơ bản: khái niệm **AMM (Automated Market Maker)**, **liquidity pool** (bể thanh khoản), **liquidity provider** (người cung cấp thanh khoản), và cơ chế định giá tự động (công thức x\*y=k).
* Biết được **lợi ích của DEX**: giao dịch không cần trung gian, ai cũng có thể niêm yết token (permissionless listing), người dùng giữ quyền kiểm soát tài sản trong suốt quá trình.
* Thảo luận **tại sao DEX quan trọng trong Web3**: DEX hiện thực hóa tài chính phi tập trung (DeFi), giúp hoàn thiện hệ sinh thái không cần ngân hàng hay sàn tập trung, đồng thời tạo nền tảng cho nhiều ứng dụng tài chính sáng tạo (yield farming, lending, v.v.).

### Nội dung chính

* **Giới thiệu DEX và Uniswap:** Uniswap là **sàn giao dịch phi tập trung (DEX)** trên Ethereum, cho phép người dùng swap (hoán đổi) token ERC-20 **mà không cần qua bất kỳ trung gian nào**. Ra mắt năm 2018, Uniswap tiên phong cho cơ chế AMM, và nhanh chóng trở thành DEX hàng đầu với khối lượng giao dịch lớn, TVL cao. Hiện Uniswap vẫn nằm top các sàn phi tập trung với hàng tỷ USD thanh khoản khóa trong các pool.
* **CEX vs DEX (so sánh ngắn):**

  * *CEX (Centralized Exchange)*: ví dụ Binance, Coinbase. Người dùng phải tạo tài khoản, nạp tiền vào ví sàn (tài sản do sàn giữ hộ), giao dịch qua sổ lệnh (order book) khớp lệnh mua-bán. Ưu: tốc độ nhanh, giao diện thân thiện, có hỗ trợ. Nhược: tập trung nên có rủi ro (bị hack sàn, sàn phá sản như Mt.Gox, FTX), phải tin tưởng sàn, và thường chỉ niêm yết các coin/token đã qua kiểm duyệt.
  * *DEX*: người dùng giao dịch trực tiếp từ ví cá nhân qua smart contract, **không cần tin cậy bên thứ ba**. Không cần đăng ký tài khoản hay KYC, chỉ cần kết nối ví (Metamask...). Mọi giao dịch được ghi on-chain, minh bạch. Bất cứ token nào tuân thủ chuẩn (ERC-20) đều có thể được giao dịch nếu có thanh khoản – **permissionless listing**. Rủi ro: người dùng tự quản lý tài sản (nếu thao tác sai có thể mất tiền, không ai hỗ trợ khôi phục), giao dịch on-chain có thể chậm và phí cao khi mạng tắc.
* **Nguyên lý AMM của Uniswap:**

  * Thay vì sổ lệnh, Uniswap dùng **Automated Market Maker**: mỗi cặp token có một **pool thanh khoản** do người dùng (LPs) gửi vào. Ví dụ cặp ETH/USDT có pool chứa X ETH và Y USDT. Bất kỳ ai muốn trade chỉ cần tương tác với pool: *mua ETH* tức là nạp USDT vào pool và rút bớt ETH ra, *bán ETH* thì ngược lại.
  * **Công thức x\*y=k:** Uniswap V2 dùng công thức này để đảm bảo **sản phẩm không đổi**. Nếu pool ban đầu có X \* Y = k, khi người mua rút bớt ETH (giảm X) và nạp USDT (tăng Y), tích X\*Y phải bằng k ⇒ giá ETH tăng. Ngược lại khi bán ETH vào pool, X tăng, Y giảm, giá ETH giảm. Công thức này tự động điều chỉnh giá dựa trên cung-cầu.
  * **Ví dụ số đơn giản:** Giả sử pool ban đầu có 100 ETH và 200,000 USDT (tỷ giá 1 ETH = 2000 USDT). Nếu một người mua 1 ETH từ pool, họ phải nạp \~2000 USDT, sau giao dịch pool có \~99 ETH và 202,000 USDT. Giá mới = 202000/99 ≈ 2040 USDT/ETH (tăng chút). Nếu mua nhiều ETH liên tục, giá trượt tăng dần – gọi là **slippage**.
  * **Liquidity Provider (LP):** Ai cũng có thể trở thành LP bằng cách gửi **cả hai token** vào pool theo tỷ lệ hiện tại. LP nhận về **LP token** đại diện phần đóng góp. LP được hưởng **phí giao dịch**: ví dụ Uniswap v2 thu 0.3% mỗi giao dịch, tự động chia cho LP theo tỷ lệ đóng góp. Đây là động lực kiếm lời cho người cung cấp thanh khoản. Tuy nhiên LP chịu rủi ro **tổn thất tạm thời (impermanent loss)** khi giá token biến động lệch nhiều – không đi quá sâu, chỉ cần lưu ý khái niệm.
* **Trải nghiệm người dùng trên Uniswap:**

  * Kết nối ví (VD: Metamask), chọn cặp token, nhập số lượng => smart contract sẽ tính toán và thực hiện hoán đổi. Người dùng trả một **phí gas** cho mạng Ethereum và một phần nhỏ phí giao dịch cho LP.
  * Không cần tạo tài khoản, không ai có thể ngăn giao dịch của bạn (trừ khi token đó không có pool thanh khoản).
  * Giao dịch xong, token mới vào ví của người dùng, không phải rút ra từ sàn như CEX.
* **Sự phát triển của DEX:**

  * Uniswap mở đầu, sau đó nhiều DEX khác ra đời: SushiSwap (fork từ Uni nhưng có token quản trị), PancakeSwap (trên BSC), Trader Joe (Avalanche), v.v. Mô hình AMM được cải tiến (Uniswap v3 với *concentrated liquidity* cho phép LP chọn dải giá).
  * Khái niệm **yield farming**: 2020 t.g gọi là “Mùa hè DeFi”, các dự án khuyến khích cung cấp thanh khoản bằng cách thưởng token, dẫn tới bùng nổ người dùng DEX.
  * **Khối lượng giao dịch DEX** tăng mạnh; có thời điểm (2021) volume Uniswap còn vượt cả Coinbase – chứng minh sức mạnh của mô hình phi tập trung.
* **Tại sao DEX quan trọng trong Web3:**

  * **Tự chủ tài sản:** Triết lý “not your keys, not your coins” – dùng DEX, người dùng luôn giữ private key, giảm rủi ro mất tiền do sàn sập/hack.
  * **Permissionless innovation:** Bất cứ token mới nào (startup Web3) đều có thể tạo thị trường thanh khoản mà không cần thuyết phục sàn lớn niêm yết. Điều này thúc đẩy **hệ sinh thái DeFi** phong phú.
  * **Censorship resistance:** DEX khó bị đóng cửa hơn CEX (vì là smart contract chạy phân tán). Ngay cả khi website bị chặn, người dùng vẫn có thể tương tác trực tiếp với hợp đồng nếu rành kỹ thuật, hoặc thông qua các giao diện khác (do mã nguồn mở nên nhiều giao diện có thể kết nối).
  * **Tài chính mở 24/7 toàn cầu:** Bất kỳ ai trên thế giới, bất kỳ lúc nào, đều có thể giao dịch nếu có internet + ví, không phụ thuộc múi giờ thị trường, không cần đăng ký.
  * **Nền tảng cho DeFi phức tạp:** DEX là mảnh ghép cơ bản, trên đó mới xây dựng được các thứ như aggregator (gộp nhiều DEX tìm giá tốt nhất), lending (vay thế chấp token), stablecoin (swap stable), phái sinh phi tập trung, v.v. Nếu thiếu DEX, Web3 tài chính sẽ kém hoàn thiện.

### Cấu trúc buổi học

1. **Khởi động (5 phút):** Hỏi: *“Ai ở đây từng mua Bitcoin/ETH trên sàn như Binance chưa? Trải nghiệm thế nào?”*. Để vài người chia sẻ (đăng ký, chờ KYC, nộp tiền...). Sau đó hỏi: *“Có cách nào trade crypto **không cần sàn** không?”*. Giới thiệu: *“Đó chính là DEX – và Uniswap là ví dụ tiêu biểu.”*
2. **Trình bày khái niệm DEX (5 phút):** Định nghĩa DEX, so sánh nhanh với CEX. Nhấn mạnh từ khóa **“không cần trung gian, giao dịch thẳng từ ví”**. Có thể chiếu một bảng so sánh CEX vs DEX (sử dụng các ý đã liệt kê ở trên) để trực quan.
3. **Giải thích cơ chế Uniswap (15 phút):** Dùng bảng hoặc slide minh họa **pool**. Vẽ hai thùng nước (hoặc hai cột tài sản) tượng trưng cho pool token A và B. Minh họa người trade bằng cách lấy từ thùng này đổ sang thùng kia. Trình bày công thức x\*y=k một cách đơn giản, tránh công thức phức tạp: chỉ cần nói “mỗi lần giao dịch, tỷ lệ token trong pool thay đổi -> giá thay đổi tương ứng để giữ tổng giá trị cân bằng”. Có thể đưa một ví dụ số nhỏ (như trên).

   * Nhớ giải thích vai trò **người cung cấp thanh khoản**: dùng ẩn dụ *“họ như người đổ nước vào thùng để tạo hồ bơi; và được thưởng phí như tiền vé của người bơi”*.
   * Cho xem giao diện Uniswap (nếu mạng cho phép): mở app.uniswap.org, nhập một cặp token (ví dụ ETH-USDT) để thấy tỷ giá, trường nhập số lượng, phần hiển thị dự tính trượt giá, phí. (Không cần thực hiện swap thật nếu ko có ví, chỉ minh họa UI).
   * Giải thích khái niệm **slippage** (trượt giá) khi giao dịch khối lượng lớn so với pool – có thể ví: *“bạn múc nhiều nước từ bể, mực nước giảm đáng kể nên nồng độ thay đổi nhiều”*.
4. **Ví dụ thực tế (5 phút):** Nếu có sẵn ví (testnet hoặc chứa ít token trên mainnet), có thể làm thử một giao dịch nhỏ trên Uniswap trước lớp và chiếu transaction đó (hoặc trình bày bước thực hiện). Nếu không, cho xem một **tx hash trên Etherscan** của giao dịch swap, highlight các thông tin: số lượng in/out, phí gas, v.v. Điều này giúp học viên thấy DEX giao dịch thực sự diễn ra on-chain chứ không phải trong sổ cái riêng của sàn.
5. **Thảo luận ưu/nhược (10 phút):** Hỏi lớp:

   * *“Ưu điểm của DEX là gì?”* – Mong đợi: an toàn (ko sợ sàn sập), tự do (nhiều token), ẩn danh (ko KYC).
   * *“Nhược điểm thì sao?”* – Mong đợi: chậm hơn (phải chờ block), phí cao (lúc tắc network), giao diện phức tạp hơn, không có ai hỗ trợ nếu sai, có thể gặp **scam token** (token giả mạo giống tên, người dùng trade nhầm).
   * Nhân đây, giảng viên giải thích chiêu **scam token**: vì DEX ai cũng list token được, nên xuất hiện token nhái (ví dụ “UNI” giả) – người dùng phải kiểm tra contract address cẩn thận khi giao dịch.
6. **Tổng kết vai trò (5 phút):** Nhấn mạnh: Uniswap và DEX nói chung là trụ cột của DeFi – tạo nên một **thị trường mở** 24/7 cho tài sản crypto. Liên hệ bức tranh lớn: *“Trước đây ta có tiền (Bitcoin), có máy tính (Ethereum), giờ có chợ (Uniswap). Dần dần, hệ sinh thái tài chính phi tập trung hoàn chỉnh hình thành.”* Bật mí nội dung buổi cuối: *“Chúng ta đã có nhiều blockchain khác nhau, vậy làm sao kết nối chúng? Buổi sau sẽ về Bridge & LayerZero.”*

### Tài nguyên giảng dạy

* **Bài viết giới thiệu:** *“Uniswap (UNI) là gì? Tìm hiểu về sàn DEX hàng đầu…”* (Coin68, 2023) – mô tả dễ hiểu Uniswap, cơ chế AMM, sự phát triển, có thống kê TVL, khối lượng.
* **Bài viết học thuật hơn:** *“Mô hình hoạt động Uniswap V2 – Nền tảng của các AMM”* (Coin98 Insights) – giải thích chi tiết công thức x\*y=k, ví dụ số và cả mã nguồn pseudo. Thích hợp cho giảng viên nghiên cứu trước để tự tin giải thích.
* **Video hướng dẫn:** *“Cách sử dụng Uniswap cho người mới”* (YouTube, tiếng Việt) – quay màn hình thao tác swap trên Uniswap và giải thích các bước. Giảng viên có thể trích một đoạn để chiếu (ví dụ đoạn nói về kết nối ví và chọn token).
* **Dữ liệu thực:** Trang **DefiLlama** – thống kê khối lượng giao dịch DEX, thị phần Uniswap. Có thể lấy một con số nhỏ cho vui (ví dụ: “24h qua Uniswap giao dịch X tỷ USD, trong khi sàn X giao dịch Y tỷ”).
* **Bài học kinh nghiệm:** Case study ngắn về sự kiện *“FTX sập 2022”* – nhiều người mất tiền vì sàn tập trung. Nêu sự kiện này để nhấn mạnh lại giá trị phi tập trung: nếu ai cũng tự giữ coin và dùng DEX, sẽ không có chuyện sập sàn mất tiền. (Nguồn: các báo crypto cuối 2022).

### Hướng dẫn giảng dạy

* **Diễn giải bằng câu chuyện:** Có thể kể câu chuyện của **Hayden Adams** – người sáng lập Uniswap: anh ấy thất nghiệp, học lập trình Solidity theo bài blog của Vitalik, rồi xây Uniswap chỉ với một ý tưởng đơn giản. Cộng đồng dùng ngày càng đông, Uniswap thành công. Câu chuyện này truyền cảm hứng: *“Một cá nhân với ý tưởng hay + môi trường mở Ethereum = tạo ra sản phẩm tỉ đô trong DeFi.”* (Khích lệ tinh thần startup Web3).
* **Trò chơi nhỏ minh họa AMM:** Nếu lớp không quá đông, có thể làm trò chơi: chọn 2 học viên đại diện cho pool (một bạn cầm 10 kẹo, một bạn cầm 10 bút giả làm 2 token). Mời một “trader” đưa 2 kẹo để đổi lấy một số bút theo tỷ lệ hiện tại (ban đầu 1 kẹo = 1 bút). Khi bút giảm, giá kẹo tăng... Làm vài lượt để cả lớp thấy “giá” thay đổi thế nào. Hoạt động vui giúp ghi nhớ.
* **Nhấn mạnh thực hành an toàn:** Hướng dẫn học viên (nếu họ tự dùng sau này) lưu ý: kiểm tra kỹ địa chỉ token trước khi swap (tránh token giả), chú ý thiết lập slippage tolerance, và cẩn thận với phê duyệt (approve) token vô hạn (có thể bị hack nếu contract xấu). Đây là kiến thức nâng cao hơn, nhưng ít nhất đề cập để họ biết DEX cũng cần kỹ năng sử dụng an toàn.
* **Liên hệ kiến thức cũ:** Permissionless – nhắc lại: Uniswap listing permissionless, bất kỳ token ERC-20 đều giao dịch được. Smart contract – đây chính là ứng dụng cụ thể: code Uniswap tự động làm vai trò market maker. Web3 vision – DEX là “ngân hàng/trung tâm tài chính phi tập trung”.
* **Khuyến khích dùng thử (cẩn thận):** Nếu công ty cho phép, có thể khuyến khích học viên thử tạo ví và dùng Uniswap với số tiền nhỏ (trên testnet càng tốt) để tự trải nghiệm. Trải nghiệm thực tế sẽ giúp họ hiểu sâu sắc cách DEX hoạt động, nhưng phải dặn dò an toàn (như không dùng ví cá nhân chứa nhiều tiền, đề phòng phishing).

### Câu hỏi thảo luận gợi ý

* **So với giao dịch trên sàn Binance, giao dịch trên Uniswap khác những gì?** – Học viên liệt kê: không cần nạp tiền vào sàn, dùng ví cá nhân; không có lệnh mua/bán mà swap ngay; phải trả phí gas; chọn token tùy ý (nhiều lựa chọn hơn)… Câu này kiểm tra hiểu biết vừa học.
* **Điều gì đảm bảo người dùng A có thể mua token từ người dùng B trên DEX mà không cần họ gặp nhau?** – Gợi họ giải thích vai trò **pool thanh khoản**. Đáp: vì đã có pool, người mua bán chỉ tương tác với pool chứ không cần khớp trực tiếp với nhau như sàn order book.
* **Ai là người định giá token trên Uniswap?** – Học viên có thể lúng túng, giảng viên hướng: *“Có phải một tổ chức hay thuật toán AI định giá không?”* – Để dẫn đến câu trả lời: **công thức AMM** định giá dựa trên số lượng trong pool, tức là *chính người giao dịch gián tiếp quyết định giá* (mua nhiều thì giá tăng, bán nhiều giá giảm).
* **Những rủi ro nào khi cung cấp thanh khoản kiếm phí trên Uniswap?** – Câu này nâng cao hơn, nhưng khuyến khích tư duy: học viên có thể nói về impermanent loss nếu biết (nếu không, giảng viên giải thích sơ: khi tỷ giá 2 token biến động, LP có thể lỗ so với chỉ giữ token). Cũng có thể nói đến rủi ro smart contract (dù Uniswap đã kiểm định, nhưng nguyên tắc DeFi: hợp đồng lỗi có thể mất tiền). Ý thức được rủi ro giúp họ không lầm tưởng “DeFi = lợi nhuận vô rủi ro”.
* **Bạn có nghĩ DEX sẽ thay thế hoàn toàn sàn tập trung không? Tại sao?** – Một câu mở. Có người sẽ nói có (vì triết lý phi tập trung), có người nói không (vì người mới vẫn cần giao diện thân thiện, CEX cung cấp fiat onramp...). Hãy để họ tranh luận. Giảng viên kết luận: có lẽ cả hai sẽ cùng tồn tại, nhưng DEX chắc chắn sẽ ngày càng quan trọng, đặc biệt đối với cộng đồng thuần crypto.

---