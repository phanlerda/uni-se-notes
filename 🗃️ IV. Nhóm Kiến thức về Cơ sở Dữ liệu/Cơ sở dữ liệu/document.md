

---

## 📚 **HỆ THỐNG CƠ SỞ DỮ LIỆU (DATABASE SYSTEMS)** 📚
*Tài liệu của Nguyễn Văn Diêu - HO CHI MINH CITY UNIVERSITY OF TRANSPORT - 2020*

---

### **PHẦN 1: TỔNG QUAN VỀ CSDL (OVERVIEW)**

#### 🎯 **1.1. Mục tiêu học tập (Learning Objectives)**
*   Định nghĩa Cơ sở dữ liệu (CSDL - Database) và Hệ Quản trị CSDL (DBMS).
*   Nghiên cứu cấu trúc của mô hình quan hệ trong CSDL.
*   Truy vấn dữ liệu bằng ngôn ngữ Đại số Quan hệ và SQL.
*   Phân tích các Ràng buộc Toàn vẹn Dữ liệu.
*   (Ứng dụng) Python GUI cho CSDL.

#### 🌍 **1.2. CSDL ở mọi nơi (Databases Are Everywhere)**
*   **CSDL:** Là một tập hợp lớn (?) các dữ liệu có liên quan.
*   **Mô hình hóa:** CSDL mô hình hóa một tổ chức trong thế giới thực (ví dụ: doanh nghiệp, trường học).
    *   **Thực thể (Entities):** Ví dụ: sinh viên, khóa học.
    *   **Mối quan hệ (Relationships):** Ví dụ: "Martin đang dạy môn CSDL học kỳ 2018/09".
*   **Thay đổi:** Thay đổi trong tổ chức dẫn đến thay đổi trong CSDL.
*   **Ví dụ ứng dụng:**
    *   Hồ sơ nhân sự.
    *   Quản lý sinh viên.
    *   Ngân hàng.
    *   Đặt vé máy bay.

####🔬 **1.3. CSDL Khoa học (Scientific Databases - Examples)**
*   **Sinh học:** Chuỗi DNA, chuỗi amino acid của protein, gen biểu hiện trong mô (hàng Gigabytes).
*   **Thiên văn học:** Vị trí và quang phổ của các thiên thể (hàng Terabytes).
*   **Vật lý:** Dữ liệu cảm biến từ các thí nghiệm vật lý hạt (hàng Petabytes).

#### 🔩 **1.4. Các thao tác với CSDL (Operations with Databases)**
1.  **Thiết kế (Design):**
    *   Định nghĩa cấu trúc và kiểu dữ liệu.
2.  **Xây dựng (Construction):**
    *   Tạo cấu trúc dữ liệu của CSDL.
    *   Nạp dữ liệu (populate) vào CSDL.
3.  **Thao tác dữ liệu (Manipulation of Data):**
    *   **Chèn (Insert), Xóa (Delete), Cập nhật (Update).**
    *   **Truy vấn (Query):** Ví dụ: "Phòng ban nào trả lương cao nhất?".
    *   **Tạo báo cáo (Create reports):** Ví dụ: "Liệt kê lương tháng của nhân viên, sắp xếp theo phòng ban, với lương trung bình và tổng lương cho mỗi phòng ban".

#### 🖥️ **1.5. Hệ Quản trị Cơ sở dữ liệu (DBMS - Database Management System)**
*   **Định nghĩa:** DBMS là một gói phần mềm được thiết kế để lưu trữ và quản lý CSDL.
*   **Các DBMS phổ biến:**
    *   Oracle (Oracle)
    *   DB2 (IBM)
    *   SQL Server, Access (Microsoft)
    *   MySQL, PostgreSQL, HSQLDB, SQLite (mã nguồn mở)

#### 👍 **1.6. Tại sao sử dụng DBMS?**
*   Tách biệt định nghĩa dữ liệu và chương trình ứng dụng.
*   Trừu tượng hóa thành mô hình đơn giản.
*   Độc lập dữ liệu và truy cập hiệu quả.
*   Giảm thời gian phát triển ứng dụng.
*   Đảm bảo tính toàn vẹn và bảo mật dữ liệu.
*   Quản trị dữ liệu đồng nhất.
*   Truy cập đồng thời, phục hồi sau sự cố.
*   Hỗ trợ nhiều khung nhìn (views) khác nhau.

#### 🤔 **1.7. Tại sao học CSDL?**
*   CSDL từng là ứng dụng chuyên biệt, nay là thành phần trung tâm trong hầu hết ứng dụng.
*   Kiến thức về CSDL là thiết yếu cho nhà khoa học máy tính.
*   CSDL có ở mọi nơi, ngay cả khi bạn không thấy chúng.
*   Dữ liệu rất có giá trị (hồ sơ thuế, sinh viên, tài khoản ngân hàng, ảnh,...).
*   Dữ liệu thường có cấu trúc (hồ sơ thuế theo cùng cấu trúc, hồ sơ ngân hàng theo cùng cấu trúc,...).
*   Lĩnh vực CSDL đã có nhiều đóng góp cho khoa học máy tính.

---

### **PHẦN 2: MÔ HÌNH DỮ LIỆU QUAN HỆ (RELATIONAL DATA MODEL)**

#### 📐 **2.1. Mô hình dữ liệu (Data Model)**
*   Là một ký hiệu để mô tả dữ liệu hoặc thông tin, thường bao gồm 3 phần:
    1.  **Cấu trúc dữ liệu (Structure of the data):**
        *   Tương tự ngôn ngữ lập trình (mảng, cấu trúc, đối tượng).
        *   Trong CSDL, mô hình dữ liệu được gọi là mô hình khái niệm để nhấn mạnh sự khác biệt về cấp độ.
    2.  **Các thao tác trên dữ liệu (Operations on the data):**
        *   Thao tác truy xuất thông tin: Tập hợp các câu truy vấn.
        *   Thao tác thay đổi CSDL: Tập hợp các sửa đổi.
    3.  **Các ràng buộc trên dữ liệu (Constraints on the data):**
        *   Cách mô tả các giới hạn về những gì dữ liệu có thể có.

#### ✨ **2.2. Các mô hình dữ liệu quan trọng (Important Data Models)**
*   **Mô hình dữ liệu quan hệ (Relational data model):** Bao gồm các mở rộng quan hệ-đối tượng.
*   **Mô hình dữ liệu bán cấu trúc (Semi-structured data model):** Bao gồm XML và các tiêu chuẩn liên quan.
*   **Mô hình dữ liệu NoSQL (NoSQL data model):** Bốn loại CSDL NoSQL chính: Document-oriented, Key-Value Pairs, Column oriented, và Graph.

#### 🖼️ **2.3. Giới thiệu Mô hình Dữ liệu Quan hệ (Relational Data Model)**
*   Biểu diễn dữ liệu bằng một cách duy nhất: **bảng hai chiều (two-dimensional table)** được gọi là **quan hệ (relation)**.
*   **Ví dụ:** Bảng `STUDENT`
    | ST-ID | ST-NAME         | CLASS-ID |
    | :---- | :-------------- | :------- |
    | S01   | Nguyen Van Nam  | L01      |
    | S02   | Nguyen Van Nam  | L01      |
    | S03   | Tran Quoc Tuan  | L01      |
    | S04   | Le Van Cuong    | L02      |
    | S05   | Nguyen Van Cuong| L02      |

#### 🏷️ **2.4. Thuộc tính (Attributes)**
*   Các cột của một quan hệ được đặt tên bằng các **thuộc tính**.
*   Một thuộc tính mô tả ý nghĩa của các mục trong cột đó.
*   Mỗi thuộc tính thuộc về một **kiểu dữ liệu (data type)**, và có một **miền giá trị (Domain)**.
*   **Miền giá trị (Domain):** Tập hợp các giá trị **nguyên tố (atomic)** có thể có, bao gồm cả giá trị `Null`.
    *   Trong miền giá trị, không cho phép cấu trúc bản ghi, tập hợp, danh sách, mảng, hoặc bất kỳ kiểu nào khác có thể chia nhỏ thành các thành phần nhỏ hơn.

#### 📜 **2.5. Lược đồ (Schemes)**
*   Tên của một quan hệ và tập hợp các thuộc tính của nó được gọi là **lược đồ quan hệ (relation scheme)**.
*   Biểu diễn lược đồ: `TEN_QUAN_HE(ThuocTinh1, ThuocTinh2, ..., ThuocTinhN)`
    *   Ví dụ: `STUDENT(ST-ID, ST-NAME, CLASS-ID)`
*   Các thuộc tính trong lược đồ quan hệ là một **tập hợp (set)**, không phải danh sách (list).
*   Một CSDL bao gồm một hoặc nhiều lược đồ quan hệ. Đây được gọi là **lược đồ CSDL quan hệ (relational database scheme)** hay đơn giản là lược đồ CSDL.
*   Tổng quát: `R( A1, A2, ..., An )`

#### ➡️ **2.6. Bộ (Tuples)**
*   Các hàng của một quan hệ được gọi là **bộ (tuples)**.
*   Một bộ có một thành phần cho mỗi thuộc tính của quan hệ.
    *   Ví dụ: bộ đầu tiên của `STUDENT` có 3 thành phần: `S01, Nguyen Van Nam, L01`.
*   Khi viết một bộ riêng lẻ, dùng dấu phẩy để tách các thành phần và dấu ngoặc đơn để bao quanh.
    *   Ví dụ: `(S01, Nguyen Van Nam, L01)`
*   Nếu `t` là một bộ, `t.Attribute` là giá trị của thuộc tính `Attribute` trong bộ `t`.
    *   Ví dụ: `t = (S01, Nguyen Van Nam, L01)` thì `t.(ST-ID) = 'S01'`.

#### 🔄 **2.7. Thể hiện Quan hệ (Relation Instances)**
*   Các bộ trong quan hệ thay đổi theo thời gian.
*   Một tập hợp các bộ cho một quan hệ tại một thời điểm nhất định là một **thể hiện (instance)** của quan hệ đó.
*   Ký hiệu: `r(R)` là thể hiện của quan hệ `R`.
*   Ví dụ: `STUDENT(ST-ID, ST-NAME, CLASS-ID)` tại một thời điểm có thể hiện như bảng ở mục 2.3.

#### 🔑 **2.8. Khóa (Keys)**
*   Một **khóa (key)** của quan hệ `R` là một tập con `K` của các thuộc tính của `R` sao cho:
    1.  Với bất kỳ hai bộ phân biệt `t1` và `t2` trong `r(R)`, thì `t1(K) ≠ t2(K)` (tính duy nhất).
    2.  Không có tập con thực sự `K'` nào của `K` có tính chất này (tính tối thiểu). *Đây là định nghĩa của Khóa Ứng Viên (Candidate Key)*.
*   `X` là một **siêu khóa (superkey)** của `R` nếu `X` chứa một khóa của `R`.
*   Trong `R` có thể có nhiều hơn một khóa (ứng viên).
*   Mỗi khóa (thường là khóa chính) được **gạch chân** trong lược đồ.
*   Ví dụ: `STUDENT` có một khóa là `ST-ID`. Lược đồ: `STUDENT(ST-ID, ST-NAME, CLASS-ID)`

---

### **PHẦN 3: ĐẠI SỐ QUAN HỆ (RELATIONAL ALGEBRA)**

#### 🧮 **3.1. Tổng quan về Đại số Quan hệ**
Các phép toán của đại số quan hệ truyền thống được chia thành các lớp chính:
1.  **Phép toán tập hợp (Set operations):** Phép hợp (union), giao (intersection), và hiệu (difference). Áp dụng cho các quan hệ.
2.  **Loại bỏ các phần của quan hệ (Remove parts):** Phép chọn (Selection) và phép chiếu (Projection).
3.  **Kết hợp các bộ của hai quan hệ (Combine tuples):** Tích Đề-các (Cartesian product), Phép kết nối (Join).
4.  **Đổi tên (Renaming):** Thay đổi lược đồ quan hệ.
5.  **Gom nhóm (Group).**
6.  ... (Các phép toán mở rộng khác)

#### ⚠️ **3.2. Điều kiện cho các phép toán tập hợp**
Cho hai quan hệ `R` và `S`, để thực hiện phép toán tập hợp, cần các điều kiện:
1.  Tập thuộc tính phải giống hệt nhau, miền giá trị cho mỗi thuộc tính tương ứng phải giống nhau.
2.  Thứ tự các thuộc tính phải giống nhau cho cả hai quan hệ (khả tương hợp về kiểu).

#### ➕➖∩ **3.3. Các phép toán tập hợp (Set Operators)**
Cho `R` và `S` là các tập hợp các bộ (quan hệ):
1.  **Phép Hợp (Union):** `R ∪ S = {t | t ∈ r(R) ∨ t ∈ s(S)}`
    *   Kết quả chứa tất cả các bộ có trong `R` hoặc trong `S` (hoặc cả hai). Loại bỏ trùng lặp.
2.  **Phép Giao (Intersection):** `R ∩ S = {t | t ∈ r(R) ∧ t ∈ s(S)}`
    *   Kết quả chứa các bộ chỉ xuất hiện trong cả `R` và `S`.
3.  **Phép Hiệu (Difference):** `R − S = {t | t ∈ r(R) ∧ t ∉ s(S)}`
    *   Kết quả chứa các bộ có trong `R` nhưng không có trong `S`.

#### σ **3.4. Phép Chọn (Selection - σ)**
*   Cho quan hệ `R` và biểu thức điều kiện logic `C`.
*   `C` được tạo từ các toán tử logic: `=`, `≠`, `<`, `≤`, `>`, `≥`, `AND (∧)`, `OR (∨)`, `NOT`.
*   Phép chọn áp dụng cho `R` tạo ra một quan hệ mới với một tập con các bộ của `r(R)`.
*   Các bộ trong quan hệ kết quả là những bộ thỏa mãn điều kiện `C` liên quan đến các thuộc tính của `R`.
*   Ký hiệu: `σ_C(R)`
*   Định nghĩa: `σ_C(R) = {t | t ∈ r(R) , t thỏa mãn C}`
*   **Ví dụ (slide 22):** Cho `R(A,B,C)`. `σ_{B=3 ∧ C>1}(R)` sẽ chọn các hàng mà cột B có giá trị 3 VÀ cột C có giá trị lớn hơn 1.

#### π **3.5. Phép Chiếu (Projection - π)**
*   Cho quan hệ `R` và `X ⊆ R` (X là tập con các thuộc tính của R). Phép chiếu của `R` lên `X`:
*   Ký hiệu: `π_X(R)`
*   `π_X(R)` chỉ chứa các thuộc tính trong `X`.
*   Định nghĩa: `π_X(R) = {t.X | t ∈ r(R)}` (t.X là bộ chỉ chứa các giá trị của các thuộc tính trong X từ bộ t)
*   **Loại bỏ các bộ trùng lặp** trong `π_X(R)`.
*   Nếu `X1 ⊆ X2 ⊆ · · · ⊆ Xm`, thì `π_X1(π_X2(· · ·(π_Xm(R))· · ·)) = π_X1(R)`
*   **Ví dụ (slide 24):** Cho `R(A,B,C)`. `π_B(R)` sẽ tạo ra một quan hệ mới chỉ có cột B, với các giá trị duy nhất từ cột B của R.

#### × **3.6. Tích Đề-các (Cartesian Product - ×)**
*   Xem quan hệ `R` và `S` là tập hợp các bộ.
*   Tích Đề-các (còn gọi là cross-product, product) của hai tập `R` và `S` là tập hợp các cặp (phần tử của `R`, phần tử của `S`).
*   Ký hiệu: `R × S`
*   Quan hệ `R × S` có tất cả các thuộc tính của `R` và `S`. Nếu có thuộc tính trùng tên, cần đổi tên trước.
*   Định nghĩa: `R × S = {(t1, t2) | t1 ∈ r(R), t2 ∈ s(S)}` (trong đó (t1,t2) là một bộ mới được tạo bằng cách nối t1 và t2)
*   **Ví dụ (slide 26):** `R(A,B)` và `S(C,D)`. `R × S` sẽ có các cột `(A,B,C,D)` và mỗi hàng của R sẽ được ghép với từng hàng của S.

#### ⋈ **3.7. Phép Kết nối Tự nhiên (Natural Join - ⋈)**
*   Cho quan hệ `R` và `S` với `X = R ∩ S` (X là tập các thuộc tính chung).
*   Kết nối tự nhiên của `R` và `S` là phép ghép các bộ từ `r(R)` và `s(S)` mà **trùng khớp trên các thuộc tính chung `X`**.
*   `X` được gọi là các thuộc tính chung.
*   Ký hiệu: `R ⋈ S`
*   Định nghĩa: `R ⋈ S = { (t1, t2_phần_riêng_của_S) | t1 ∈ r(R), t2 ∈ s(S), t1.X = t2.X }`
    *   Hoặc, chính thức hơn: `R ⋈ S = π_L(σ_{R.X=S.X}(R × S))` với `L = Attributes(R) ∪ Attributes(S)` (các thuộc tính chung chỉ xuất hiện một lần).
*   Nếu `X = ∅` (không có thuộc tính chung), Phép Kết nối Tự nhiên trở thành Tích Đề-các.
*   **Ví dụ (slide 28):** `R(A,B,C)` và `S(C,D)`. Thuộc tính chung là `C`. Kết quả `R ⋈ S` sẽ có các cột `(A,B,C,D)`.

#### ⋈<sub>θ</sub> **3.8. Phép Kết nối Theta (Theta-join - ⋈<sub>θ</sub>)**
*   Kết nối Theta của quan hệ `R` và `S` dựa trên điều kiện `θ`:
*   Kết quả được xây dựng như sau:
    1.  Tính Tích Đề-các: `R × S`
    2.  Chọn các bộ từ `R × S` thỏa mãn điều kiện `θ`.
*   Ký hiệu: `R ⋈_θ S = σ_θ(R × S)`
*   `θ` là một biểu thức so sánh giữa các thuộc tính của `R` và `S`.
*   **Ví dụ (slide 30):** `R(A,B,C)`, `S(D,E)`. `R ⋈_{C>D} S` sẽ là `σ_{C>D}(R × S)`.

#### ⋉ **3.9. Phép Bán Kết nối Trái (Left Semi-join - ⋉)**
*   Cho `R` và `S`. Tương tự kết nối tự nhiên.
*   Kết quả là tập hợp tất cả các bộ trong `r(R)` mà tồn tại một bộ trong `s(S)` bằng nhau trên các thuộc tính chung của chúng.
*   Điểm khác biệt so với kết nối tự nhiên: **các thuộc tính khác của `S` không xuất hiện** trong kết quả.
*   Ký hiệu: `R ⋉ S`
*   Định nghĩa: `R ⋉ S = {t | t ∈ r(R) ∧ ∃s ∈ s(S) sao cho t và s khớp trên thuộc tính chung}`
    *   Hoặc: `R ⋉ S = π_{Attributes(R)}(R ⋈ S)`
*   **Ví dụ (slide 32):** `R(A,B,C)`, `S(C,D)`. `R ⋉ S` sẽ chỉ giữ lại các hàng từ `R` có giá trị `C` tồn tại trong `S`, và kết quả chỉ có các cột `A,B,C`.

#### ⋊ **3.10. Phép Bán Kết nối Phải (Right Semi-join - ⋊)**
*   Tương tự Left Semi-join, nhưng giữ lại các bộ từ `S` và các thuộc tính của `S`.
*   Ký hiệu: `R ⋊ S`
*   Định nghĩa: `R ⋊ S = π_{Attributes(S)}(R ⋈ S)`
*   **Ví dụ (slide 34):** `R(A,B,C)`, `S(C,D)`. `R ⋊ S` sẽ chỉ giữ lại các hàng từ `S` có giá trị `C` tồn tại trong `R`, và kết quả chỉ có các cột `C,D`.

#### ▷ **3.11. Phép Phản Kết nối (Anti-join - ▷)**
*   Cho `R` và `S`. Tương tự semi-join, nhưng kết quả là những bộ trong `R` mà **không có** bộ nào trong `S` bằng nhau trên các thuộc tính chung.
*   Ký hiệu: `R ▷ S`
*   Định nghĩa: `R ▷ S = {t | t ∈ r(R) ∧ ¬∃s ∈ s(S) sao cho t và s khớp trên thuộc tính chung}`
    *   Hoặc: `R ▷ S = R - (R ⋉ S)`
*   **Ví dụ (slide 36):** `R(A,B,C)`, `S(C,D)`. `R ▷ S` sẽ giữ lại các hàng từ `R` mà giá trị `C` của nó không xuất hiện trong cột `C` của `S`.

#### 🌳 **3.12. Truy vấn phức tạp (Complex Queries)**
*   Truy vấn phức tạp tham chiếu dữ liệu trong nhiều quan hệ.
*   Trong đại số quan hệ, có thể tạo các biểu thức bằng cách áp dụng các phép toán lên kết quả của các phép toán khác.
*   Có thể biểu diễn các biểu thức dưới dạng **cây biểu thức (expression trees)**, giúp chương trình máy tính thực thi dễ dàng.
*   **Ví dụ (slide 38):** Tìm `A` khi `B > 3` VÀ `A` khi `E < 4` từ `R(A,B,C,D,E)`.
    *   Trả lời: `π_A(σ_{B>3}(R) ∪ σ_{E<4}(R))` hoặc `π_A(σ_{B>3 ∨ E<4}(R))` (Cách thứ hai hiệu quả hơn nếu A là thuộc tính chung).

#### ρ **3.13. Phép Đổi tên (Rename - ρ)**
*   Để kiểm soát tên của các thuộc tính hoặc lược đồ quan hệ. Dữ liệu (các bộ) không thay đổi.
*   Ký hiệu: `ρ_{S(A1,A2,...,An)}(R)` đổi tên quan hệ `R` thành `S`, và `n` thuộc tính của `R` lần lượt thành `A1, A2, ..., An`.
*   Ví dụ (slide 39): Cho `R(ABC)`.
    *   `ρ_S(R)` cho quan hệ `S(ABC)`.
    *   Nếu `S(ABC)` đã có, `ρ_{ADE}(S)` cho quan hệ `S(ADE)` (tức là `A` của `S` cũ thành `A`, `B` thành `D`, `C` thành `E`).

#### := **3.14. Phép Gán (Assignment - :=)**
*   Định nghĩa: Gán một biểu thức quan hệ cho một tên quan hệ (tạm thời).
*   Ký hiệu: `:=`
*   Ví dụ (slide 40):
    *   `StudentMark(StudentID, SubjectID, Mark)`
    *   `R(T,U,M) := σ_{SubjectID='S01' ∧ Mark>7}(StudentMark)`
    *   `S(T,U,M) := σ_{SubjectID='S02' ∧ Mark>9}(StudentMark)`
    *   `Answer(StudentID) := π_T(R ∩ S)` (Tìm sinh viên có điểm môn S01 > 7 VÀ điểm môn S02 > 9)

#### ÷ **3.15. Phép Chia (Division - ÷)**
*   Phép chia có định nghĩa khá phức tạp, nhưng có ứng dụng trong các tình huống tự nhiên (ví dụ: "tìm sinh viên đã học TẤT CẢ các môn học bắt buộc").
*   Cho `R` và `S`, với các thuộc tính của `S` là tập con của các thuộc tính của `R` (`Attributes(S) ⊆ Attributes(R)`).
*   Đặt `R' = Attributes(R) - Attributes(S)` (các thuộc tính chỉ có trong R).
*   `R` chia cho `S`, viết là `R ÷ S`.
*   Kết quả `r'(R') = {t | với mọi bộ ts ∈ s(S), tồn tại một bộ tr ∈ r(R) sao cho tr(R') = t và tr(Attributes(S)) = ts}`.
    *   Nghĩa là: một bộ `t` (chỉ gồm các thuộc tính `R'`) nằm trong kết quả nếu nó kết hợp với *mọi* bộ trong `S` để tạo thành một bộ có trong `R`.
*   **Ví dụ (slide 42):** `R(A,B)` và `S(B)`. `R'(A) = R(A,B) ÷ S(B)`.
    *   Nếu `S` có các giá trị `B` là `1, 2`.
    *   `R` có `(7,1), (7,2), (5,1), (5,2), (8,1)`.
    *   Kết quả `R'(A)` sẽ là `{ (7), (5) }` vì A=7 xuất hiện với cả B=1 và B=2; A=5 cũng vậy. A=8 chỉ xuất hiện với B=1, không đủ.

#### 🔗 **3.16. Phép Kết nối Ngoài (Outer Joins)**
*   Giá trị `Null` là giá trị không xác định hoặc không tồn tại.
*   Mọi so sánh liên quan đến `Null` đều trả về `false` theo định nghĩa (trong ngữ cảnh so sánh chuẩn, SQL có `IS NULL`).
*   Mở rộng của phép kết nối để tránh mất thông tin.
*   Tính toán phép kết nối, sau đó thêm các bộ từ một quan hệ không khớp với các bộ trong quan hệ kia vào kết quả của phép kết nối (điền `Null` vào các thuộc tính thiếu).

    *   **3.17. Phép Kết nối Ngoài Trái (Left Outer Join - ▷◁ (ký hiệu slide))**
        *   Ký hiệu: `R ▷◁ S` (SQL: `R LEFT OUTER JOIN S ON condition`)
        *   Kết quả bao gồm:
            1.  Các bộ trong `R` và `S` bằng nhau trên thuộc tính chung (như Natural Join).
            2.  Thêm các bộ trong `R` không có bộ nào khớp trong `S` (các cột từ `S` sẽ là `Null`).
        *   Công thức (slide 44): `(R ⋈ S) ∪ ((R - π_R(R ⋈ S)) × {(⊥, ..., ⊥)})` (⊥ là Null, áp dụng cho các thuộc tính chỉ có ở S).
        *   **Ví dụ (slide 45):** `R(A,B)`, `S(B,C)`.

    *   **3.18. Phép Kết nối Ngoài Phải (Right Outer Join - ◁◁ (ký hiệu slide))**
        *   Ký hiệu: `R ◁◁ S` (SQL: `R RIGHT OUTER JOIN S ON condition`)
        *   Tương tự Left Outer Join, nhưng ưu tiên giữ lại tất cả các bộ từ `S`.
        *   **Ví dụ (slide 47):** `R(A,B)`, `S(B,C)`.

    *   **3.19. Phép Kết nối Ngoài Đầy đủ (Full Outer Join - ▷◁▷ (ký hiệu slide, có vẻ lỗi, thường là ▷◁ với hai vạch ngang)**
        *   Ký hiệu: `R ▷◁ S` (ký hiệu chuẩn, slide có thể khác) (SQL: `R FULL OUTER JOIN S ON condition`)
        *   Kết quả bao gồm:
            1.  Các bộ khớp từ cả `R` và `S`.
            2.  Các bộ trong `R` không khớp trong `S` (cột từ `S` là `Null`).
            3.  Các bộ trong `S` không khớp trong `R` (cột từ `R` là `Null`).
        *   Định nghĩa: `R FULL_OUTER_JOIN S = (R LEFT_OUTER_JOIN S) ∪ (R RIGHT_OUTER_JOIN S)` (cần cẩn thận loại bỏ trùng lặp phần natural join).
        *   **Ví dụ (slide 49):** `R(A,B)`, `S(B,C)`.

#### δ **3.20. Phép Loại bỏ Trùng lặp (Duplicate Elimination Operators - δ)**
*   Cho `R`.
*   Ký hiệu: `δ(R)`
*   Trả về tập hợp bao gồm **một bản sao** của mỗi bộ xuất hiện một hoặc nhiều lần trong quan hệ `R`. (Lưu ý: Đại số quan hệ chuẩn dựa trên lý thuyết tập hợp, vốn dĩ không có trùng lặp. Phép toán này hữu ích khi làm việc với multiset/bag).
*   **Ví dụ (slide 50):** Nếu `R` có các bộ `(1,2,3), (4,5,6), (1,2,3)`. Thì `δ(R)` sẽ là `{(1,2,3), (4,5,6)}`.

#### Σ **3.21. Hàm Tổng hợp (Aggregate functions)**
*   Hàm tổng hợp nhận một tập hợp các giá trị và trả về một giá trị duy nhất.
    *   `sum(·)`: Tổng các giá trị.
    *   `avg(·)`: Giá trị trung bình.
    *   `min(·)`: Giá trị nhỏ nhất.
    *   `max(·)`: Giá trị lớn nhất.
    *   `count(·)`: Số lượng giá trị.

#### 𝒢 **3.22. Phép Gom nhóm (Group - 𝒢)**
*   Cho `U` là một biểu thức đại số quan hệ.
*   `g1, g2, ..., gn`: Các thuộc tính để gom nhóm (có thể rỗng).
*   Mỗi `fi` là một hàm tổng hợp.
*   Mỗi `Ai` là một tên thuộc tính (cho kết quả của hàm tổng hợp).
*   Ký hiệu: `g1,g2,...,gn 𝒢 f1(A1),f2(A2),...,fm(Am) (U)`
*   Thực hiện:
    1.  Phân hoạch các bộ của `U` thành các nhóm dựa trên `g1, g2, ..., gn`.
    2.  Với mỗi nhóm:
        *   Kết quả bao gồm giá trị các thuộc tính gom nhóm.
        *   Áp dụng các hàm tổng hợp `fi` cho các giá trị trong nhóm đó.
*   **Ví dụ (slide 53-54):** `R(A,B,C)`. `𝒢_{sum(A), min(B), count(C)}(R)` (nếu không có thuộc tính gom nhóm) hoặc `A 𝒢_{min(B), max(B), Count(A)}(R)` (gom nhóm theo A).

#### τ **3.23. Phép Sắp xếp (Sorting Operator - τ)**
*   Cho `R`, với `L ⊆ Attributes(R)`.
*   Sắp xếp dữ liệu trong `r(R)` theo các thuộc tính `L`.
*   Ký hiệu: `τ_L(R)`
*   **Ví dụ (slide 55):** `R(A,B,C)`. `τ_{A,B}(R)` sắp xếp các bộ của `R` theo `A` trước, sau đó theo `B`.

---

### **PHẦN 4: NGÔN NGỮ TRUY VẤN CÓ CẤU TRÚC (SQL - STRUCTURED QUERY LANGUAGE)**

#### 💬 **4.1. Giới thiệu SQL**
*   **SQL** (phát âm là "sequel") - "Structured Query Language" là ngôn ngữ chính được sử dụng để mô tả và thao tác CSDL quan hệ.
*   Có hai khía cạnh chính của SQL:
    1.  **Ngôn ngữ con Định nghĩa Dữ liệu (DDL - Data-Definition Language):** Dùng để khai báo các lược đồ CSDL.
    2.  **Ngôn ngữ con Thao tác Dữ liệu (DML - Data-Manipulation Language):** Dùng để truy vấn CSDL và sửa đổi CSDL.

#### 📋 **4.2. Các loại Quan hệ trong SQL (Relations in SQL)**
SQL phân biệt ba loại quan hệ:
1.  **Bảng (Table):** Quan hệ tồn tại trong CSDL và có thể được sửa đổi bằng cách thay đổi các bộ của nó, cũng như được truy vấn. *Đây là dữ liệu được lưu trữ vật lý.*
2.  **Khung nhìn (View):** Quan hệ được định nghĩa bởi một phép tính toán (một câu truy vấn). Các quan hệ này không được lưu trữ, mà được xây dựng (toàn bộ hoặc một phần) khi cần thiết.
3.  **Bảng tạm (Temporary table):** Được xây dựng bởi bộ xử lý ngôn ngữ SQL khi nó thực hiện công việc thực thi các truy vấn và sửa đổi dữ liệu. Các quan hệ này sau đó bị loại bỏ và không được lưu trữ.

#### 🆕 **4.3. Tạo Bảng (Create Table)**
*   **Cú pháp cơ bản:**
    ```sql
    CREATE TABLE ten_bang (
        cot1 kieu_du_lieu [rang_buoc_cot],
        cot2 kieu_du_lieu [rang_buoc_cot],
        ...,
        cotN kieu_du_lieu [rang_buoc_cot],
        PRIMARY KEY (mot_hoac_nhieu_cot),
        [rang_buoc_bang_khac]
    );
    ```
*   **Ví dụ (slide 58):**
    ```sql
    CREATE TABLE Company (
        ID INT PRIMARY KEY,
        Name TEXT NOT NULL,
        Age INT NOT NULL,
        Address CHAR(50),
        Salary REAL
    );
    ```

#### 🗑️🔄 **4.4. Xóa Bảng (Drop Table), Sửa đổi Bảng (Alter Table)**
*   **Xóa bảng:**
    ```sql
    DROP TABLE ten_bang;
    ```
*   **Sửa đổi bảng (`ALTER TABLE`):** Dùng để thêm, xóa, hoặc sửa đổi cột trong bảng hiện có. Cũng dùng để thêm và xóa các ràng buộc khác nhau trên bảng.
    *   **Thêm cột (ADD Column):**
        ```sql
        ALTER TABLE ten_bang
        ADD ten_cot kieu_du_lieu;
        ```
    *   **Xóa cột (DROP Column):**
        ```sql
        ALTER TABLE ten_bang
        DROP COLUMN ten_cot;
        ```
    *   **Sửa đổi cột (ALTER COLUMN - *tùy DBMS, ví dụ này cho SQL Server/MySQL*):**
        ```sql
        -- SQL Server / MS Access
        ALTER TABLE Persons
        ALTER COLUMN DateOfBirth YEAR;

        -- MySQL / Oracle (trước 10g)
        ALTER TABLE Persons
        MODIFY COLUMN DateOfBirth YEAR;

        -- Oracle 10g trở lên
        ALTER TABLE Persons
        MODIFY DateOfBirth YEAR;
        ```
        *(Slide 60 có ví dụ `ALTER COLUMN DateOfBirth year;` có thể đặc thù cho một DBMS cụ thể, ví dụ như SQL Server. SQLite có hỗ trợ hạn chế cho `ALTER TABLE`, chủ yếu là `RENAME TABLE`, `ADD COLUMN`, và `RENAME COLUMN` (trong phiên bản mới), `DROP COLUMN` (trong phiên bản mới). Để thay đổi kiểu dữ liệu hoặc ràng buộc phức tạp hơn, thường phải tạo bảng mới, sao chép dữ liệu, xóa bảng cũ, đổi tên bảng mới).*

*   **Ví dụ (slide 60):**
    ```sql
    CREATE TABLE contacts (
        id INTEGER PRIMARY KEY,
        name TEXT NOT NULL COLLATE NOCASE, -- COLLATE NOCASE: không phân biệt hoa thường khi so sánh
        phone TEXT NOT NULL DEFAULT 'Unknown',
        UNIQUE (name, phone) -- Ràng buộc UNIQUE trên cặp (name, phone)
    );

    DROP TABLE Shippers;

    ALTER TABLE Customers
    ADD Email VARCHAR(255);

    ALTER TABLE Customers
    DROP COLUMN Email;
    ```

#### ✨ **4.5. Chèn Dữ liệu (Insert)**
*   **Chèn một hàng:**
    ```sql
    INSERT INTO ten_bang (cot1, cot2, ...)
    VALUES (gia_tri1, gia_tri2, ...);
    ```
*   **Chèn nhiều hàng (cú pháp chuẩn, một số DBMS có thể có biến thể):**
    ```sql
    INSERT INTO ten_bang (cot1, cot2, ...)
    VALUES
        (gia_tri1_hang1, gia_tri2_hang1, ...),
        (gia_tri1_hang2, gia_tri2_hang2, ...),
        ...;
    ```
*   **Ví dụ (slide 62):**
    ```sql
    INSERT INTO Students (name)
    VALUES ('Bud Powell');

    INSERT INTO Students (name)
    VALUES
        ('Buddy Rich'),
        ('Candido'),
        ('Charlie Byrd');
    ```

#### ✍️ **4.6. Cập nhật Dữ liệu (Update)**
*   **Cú pháp:**
    ```sql
    UPDATE ten_bang
    SET cot1 = gia_tri_moi1,
        cot2 = gia_tri_moi2,
        ...
    WHERE dieu_kien_tim_kiem;
    ```
*   Điều kiện tìm kiếm trong `WHERE` thường có dạng: `Bieu_thuc_trai Toan_tu_so_sanh Bieu_thuc_phai`
*   **Ví dụ `WHERE` (slide 63):**
    *   `WHERE column1 = 100;`
    *   `WHERE column2 IN (1,2,3);`
    *   `WHERE column3 LIKE 'An%';` (Tìm chuỗi bắt đầu bằng 'An')
    *   `WHERE column4 BETWEEN 10 AND 20;`
*   **Ví dụ `UPDATE` (slide 66):**
    ```sql
    UPDATE employees
    SET lastname = 'Smith'
    WHERE employeeid = 3;

    UPDATE employees
    SET city = 'Toronto',
        state = 'ON',
        postalcode = 'M5P 2N7'
    WHERE employeeid = 4;
    ```

#### ⚖️ **4.7. Các Toán tử So sánh (Comparison Operators)**
| Operator | Meaning                      |
| :------- | :--------------------------- |
| `=`      | Bằng                         |
| `<>` or `!=` | Không bằng                   |
| `<`      | Nhỏ hơn                     |
| `>`      | Lớn hơn                     |
| `<=`     | Nhỏ hơn hoặc bằng            |
| `>=`     | Lớn hơn hoặc bằng            |

#### 🧠 **4.8. Các Toán tử Logic (Logical Operators)**
*(Lưu ý: 1 nghĩa là TRUE, 0 nghĩa là FALSE trong một số ngữ cảnh DBMS)*
| Operator  | Meaning                                                                                             |
| :-------- | :-------------------------------------------------------------------------------------------------- |
| `ALL`     | Trả về TRUE nếu tất cả các biểu thức con là TRUE (thường dùng với subquery).                         |
| `AND`     | Trả về TRUE nếu cả hai biểu thức là TRUE.                                                            |
| `ANY` / `SOME` | Trả về TRUE nếu bất kỳ biểu thức con nào trong một tập hợp so sánh là TRUE (thường dùng với subquery). |
| `BETWEEN` | Trả về TRUE nếu một giá trị nằm trong một khoảng.                                                   |
| `EXISTS`  | Trả về TRUE nếu một subquery trả về ít nhất một hàng.                                                |
| `IN`      | Trả về TRUE nếu một giá trị khớp với bất kỳ giá trị nào trong một danh sách hoặc subquery.            |
| `LIKE`    | Trả về TRUE nếu một giá trị khớp với một mẫu (pattern).                                              |
| `NOT`     | Đảo ngược giá trị của các toán tử khác (ví dụ: `NOT EXISTS`, `NOT IN`, `NOT BETWEEN`).                  |
| `OR`      | Trả về TRUE nếu một trong hai biểu thức là TRUE.                                                       |

#### ❌ **4.9. Xóa Dữ liệu (Delete)**
*   **Cú pháp:**
    ```sql
    DELETE FROM ten_bang
    WHERE dieu_kien_tim_kiem;
    ```
*   **Ví dụ (slide 67):**
    ```sql
    DELETE FROM employees
    WHERE name LIKE '%Santana%'; -- Xóa nhân viên có tên chứa 'Santana'
    ```

---
#### 📝 **Lược đồ CSDL ví dụ: Quản lý Đơn hàng (Order Management Database Scheme - slide 68)**
1.  `Categories(CategoryID, CategoryName, Description)`
    *   `CategoryID` là khóa chính.
2.  `Products(ProductID, ProductName, UnitPrice, CategoryID)`
    *   `ProductID` là khóa chính.
    *   `CategoryID` là khóa ngoại tham chiếu đến `Categories`.
3.  `Customers(CustomerID, CustomerName, Address, Phone, Email, Country)`
    *   `CustomerID` là khóa chính.
4.  `Orders(OrderID, OrderDate, RequiredDate, CustomerID)`
    *   `OrderID` là khóa chính.
    *   `CustomerID` là khóa ngoại tham chiếu đến `Customers`.
5.  `OrderDetails(OrderID, ProductID, UnitPrice, Quantity, Discount)`
    *   `(OrderID, ProductID)` là khóa chính phức hợp.
    *   `OrderID` là khóa ngoại tham chiếu đến `Orders`.
    *   `ProductID` là khóa ngoại tham chiếu đến `Products`.

---

#### 🔗 **4.10. Tích và Kết nối trong SQL (Products and Joins in SQL)**
*   **Ví dụ (slide 69):** Tìm tên khách hàng đã đặt hàng với `OrderID = 'D01'`.
    *   Cần 2 quan hệ: `Customers` và `Orders`.
    ```sql
    SELECT B.CustomerID, B.CustomerName
    FROM Orders AS A, Customers AS B -- Cách viết JOIN ngầm (implicit join)
    WHERE A.CustomerID = B.CustomerID
      AND A.OrderID = 'D01';
    ```
    *   Hoặc dùng `INNER JOIN` (khuyến khích hơn):
    ```sql
    SELECT B.CustomerID, B.CustomerName
    FROM Orders AS A
    INNER JOIN Customers AS B ON A.CustomerID = B.CustomerID
    WHERE A.OrderID = 'D01';
    ```
    *   Tương đương biểu thức Đại số Quan hệ: `π_{CustomerID, CustomerName}(σ_{OrderID='D01'}(Orders ⋈ Customers))`

#### ➕ **4.11. Phép Hợp (Union)**
*   **Ví dụ (slide 70):** Lấy ID và tên của tất cả sản phẩm thuộc `CategoryID = 'C01'` hoặc `'C02'`.
    ```sql
    (SELECT ProductID, ProductName
     FROM Products
     WHERE CategoryID = 'C01')
    UNION
    (SELECT ProductID, ProductName
     FROM Products
     WHERE CategoryID = 'C02');
    ```
    *   `UNION` tự động loại bỏ các hàng trùng lặp. Dùng `UNION ALL` để giữ lại tất cả.
    *   Tương đương Đại số Quan hệ:
        `π_{ProductID, ProductName}(σ_{CategoryID='C01'}(Products)) ∪ π_{ProductID, ProductName}(σ_{CategoryID='C02'}(Products))`

#### ∩ **4.12. Phép Giao (Intersection - `INTERSECT`)**
*   **Ví dụ (slide 71):** Lấy ID và tên sản phẩm được đặt bởi cả khách hàng `CustomerID = 'T01'` VÀ `CustomerID = 'T02'`.
    ```sql
    (SELECT C.ProductID, C.ProductName
     FROM Orders A, OrderDetails B, Products C
     WHERE A.CustomerID = 'T01'
       AND A.OrderID = B.OrderID -- Sửa từ OderID thành OrderID
       AND B.ProductID = C.ProductID)
    INTERSECT
    (SELECT C.ProductID, C.ProductName
     FROM Orders A, OrderDetails B, Products C
     WHERE A.CustomerID = 'T02'
       AND A.OrderID = B.OrderID -- Sửa từ OderID thành OrderID
       AND B.ProductID = C.ProductID);
    ```
    *   `INTERSECT` trả về các hàng duy nhất xuất hiện trong cả hai kết quả truy vấn.

#### ➖ **4.13. Phép Hiệu (Difference - `EXCEPT` hoặc `MINUS` tùy DBMS)**
*   **Ví dụ (slide 72):** Lấy ID và tên sản phẩm chưa bao giờ được đặt hàng.
    ```sql
    (SELECT ProductID, ProductName
     FROM Products)
    EXCEPT -- SQLite và PostgreSQL dùng EXCEPT, Oracle dùng MINUS
    (SELECT B.ProductID, B.ProductName -- Cần đảm bảo tên cột và kiểu dữ liệu khớp
     FROM OrderDetails A, Products B    -- Sửa: Bảng A là OrderDetails, B là Products
     WHERE A.ProductID = B.ProductID);
    ```
    *   Hoặc cách tốt hơn để lấy tên sản phẩm chưa được đặt hàng:
    ```sql
    SELECT P.ProductID, P.ProductName
    FROM Products P
    LEFT JOIN OrderDetails OD ON P.ProductID = OD.ProductID
    WHERE OD.OrderID IS NULL;
    -- Hoặc
    SELECT ProductID, ProductName
    FROM Products
    WHERE ProductID NOT IN (SELECT DISTINCT ProductID FROM OrderDetails);
    ```

#### 🎣 **4.14. Truy vấn con (Subqueries)**
*   **Subquery:** Một truy vấn nằm bên trong một truy vấn khác.
*   Subquery có thể có subquery con, và cứ thế tiếp tục.
*   Các cách sử dụng subquery:
    1.  **Trả về một hằng số duy nhất:** Hằng số này có thể được so sánh với giá trị khác trong mệnh đề `WHERE`.
        *   **Ví dụ (slide 74):** Tìm thông tin khách hàng đã đặt hàng `OrderID = 'D01'`.
            ```sql
            SELECT *
            FROM Customers
            WHERE CustomerID = (SELECT CustomerID
                                FROM Orders
                                WHERE OrderID = 'D01'); -- Giả định OrderID 'D01' chỉ do 1 CustomerID đặt
            ```
    2.  **Trả về một quan hệ (tập hợp các hàng/cột):** Có thể được sử dụng trong mệnh đề `WHERE` với các toán tử như `IN`, `EXISTS`, `ANY`, `ALL`.
    3.  **Xuất hiện trong mệnh đề `FROM`:** Subquery trong `FROM` phải được đặt tên (alias).

#### 📜 **4.15. Điều kiện liên quan đến Quan hệ (Conditions Involving Relations - với Subqueries)**
*   Các toán tử SQL áp dụng cho một quan hệ `R` (thường là kết quả của subquery) và tạo ra kết quả boolean.
*   Nếu so sánh với một giá trị đơn `s`, subquery `R` thường được yêu cầu trả về một quan hệ một cột.

    1.  **`EXISTS R`:** `TRUE` nếu `R` (kết quả subquery) không rỗng (có ít nhất 1 hàng).
        *   `NOT EXISTS R` là `TRUE` nếu `R` rỗng.
    2.  **`s IN R`:** `TRUE` nếu `s` bằng với một trong các giá trị trong `R` (quan hệ một cột).
        *   `s NOT IN R` là `TRUE` nếu `s` không bằng với giá trị nào trong `R`.
    3.  **`s > ALL R`:** `TRUE` nếu `s` lớn hơn *mọi* giá trị trong `R` (quan hệ một cột).
        *   Có thể dùng các toán tử so sánh khác: `<`, `<=`, `>=`, `=`, `<>`.
        *   `s <> ALL R` tương đương với `s NOT IN R`.
        *   `NOT s >= ALL R` là `TRUE` nếu `s` không phải là giá trị lớn nhất trong `R` (hoặc `s` nhỏ hơn ít nhất một giá trị trong `R`).
    4.  **`s > ANY R` (hoặc `s > SOME R`):** `TRUE` nếu `s` lớn hơn *ít nhất một* giá trị trong `R` (quan hệ một cột).
        *   Có thể dùng các toán tử so sánh khác.
        *   `s = ANY R` tương đương với `s IN R`.
        *   `NOT s > ANY R` là `TRUE` nếu `s` là giá trị nhỏ nhất trong `R` (hoặc `s` không lớn hơn bất kỳ giá trị nào trong `R`, tức `s <= mọi giá trị trong R`).

#### ➡️➡️ **4.16. Điều kiện liên quan đến Bộ (Conditions Involving Tuples)**
*   Nếu một bộ `t` có cùng số lượng thành phần (và kiểu tương thích) như một quan hệ `R`, có thể so sánh `t` và `R`.
*   Ví dụ: `t IN R` hoặc `t <> ANY R`.
*   **Lược đồ ví dụ: Quản lý Kho (Warehouse Management - slide 78)**
    1.  `Categories(CategoryID, CategoryName, Description)`
    2.  `Products(ProductID, ProductName, UnitPrice, CategoryID)`
    3.  `Warehouses(WarehouseID, Name, Address, CategoryID)`
    4.  `InStocks(WarehouseID, ProductID, Quantity)`
*   **Ví dụ (slide 79):** Tìm thông tin sản phẩm có thể được lưu trữ trong kho `WarehouseID = 'W01'`. (Giả định: một sản phẩm có thể được lưu trữ trong một kho nếu `CategoryID` của sản phẩm đó khớp với `CategoryID` của kho).
    ```sql
    SELECT *
    FROM Products
    WHERE (ProductID, CategoryID) IN -- So sánh một cặp giá trị (bộ)
          (SELECT P.ProductID, W.CategoryID -- Subquery phải trả về cặp cột tương ứng
           FROM Warehouses W, Products P     -- Logic ở đây cần xem lại: sản phẩm "có thể được lưu trữ" nghĩa là gì?
                                           -- Nếu là sản phẩm CÙNG CategoryID với kho:
           -- WHERE W.WarehouseID = 'W01' AND P.CategoryID = W.CategoryID
          );
    ```
    *Slide 79 có câu truy vấn hơi khó hiểu, mục đích là minh họa so sánh bộ. Câu truy vấn đúng hơn cho "sản phẩm có `CategoryID` khớp với `CategoryID` của kho W01" có thể là:*
    ```sql
    SELECT *
    FROM Products P
    WHERE P.CategoryID = (SELECT W.CategoryID
                          FROM Warehouses W
                          WHERE W.WarehouseID = 'W01');
    -- Hoặc nếu muốn tìm sản phẩm ĐANG CÓ trong kho W01:
    SELECT P.*
    FROM Products P
    JOIN InStocks I ON P.ProductID = I.ProductID
    WHERE I.WarehouseID = 'W01';
    ```
    *Ví dụ từ slide nhằm minh họa `(ProductID, CategoryID) IN (subquery_returns_productid_categoryid)`:*
    ```sql
    SELECT *
    FROM Products
    WHERE (ProductID, CategoryID) IN
          ( SELECT ProductID, B.CategoryID -- Chọn ProductID và CategoryID của Product
            FROM Warehouses A, Products B   -- Mà CategoryID của Product (B) khớp với CategoryID của Warehouse 'W01' (A)
            WHERE A.WarehouseID = 'W01' AND A.CategoryID = B.CategoryID
          );
    ```
    *Điều này có nghĩa là: Tìm các sản phẩm (Products.*) mà cặp (P.ProductID, P.CategoryID) của nó nằm trong danh sách các cặp (ProductID, CategoryID) của những sản phẩm có CategoryID trùng với CategoryID của kho 'W01'. Điều này khá vòng vo và có thể đơn giản hóa.*

#### ➰ **4.17. Truy vấn con Tương quan (Correlated Subqueries)**
*   Truy vấn con đơn giản nhất được đánh giá *một lần* và kết quả được sử dụng trong truy vấn cấp cao hơn.
*   **Truy vấn con lồng nhau (Nested subqueries)**, đặc biệt là **truy vấn con tương quan (correlated subquery)**, yêu cầu subquery được đánh giá *nhiều lần* - một lần cho mỗi hàng của truy vấn bên ngoài mà nó tham chiếu.
*   **Ví dụ (slide 80):** Tìm thông tin về kho và sản phẩm có trong kho (`InStock`) với `Quantity > 30`.
    ```sql
    SELECT A.*, B.*  -- A là Warehouses, B là Products
    FROM Warehouses A, Products B
    WHERE A.CategoryID = B.CategoryID -- Điều kiện kết nối giữa Kho và Sản phẩm (có thể không cần thiết nếu chỉ quan tâm InStocks)
      AND 30 < (SELECT Quantity        -- Đây là Correlated Subquery
                FROM InStocks I
                WHERE I.WarehouseID = A.WarehouseID -- Tham chiếu đến A của truy vấn ngoài
                  AND I.ProductID = B.ProductID)    -- Tham chiếu đến B của truy vấn ngoài
    ORDER BY A.WarehouseID, B.ProductID;
    ```
    *Cách viết tốt hơn và rõ ràng hơn thường dùng `JOIN` và `EXISTS` hoặc điều kiện trực tiếp:*
    ```sql
    SELECT W.*, P.*, I.Quantity
    FROM Warehouses W
    JOIN Products P ON W.CategoryID = P.CategoryID -- Nếu cần thông tin từ cả 3 bảng
    JOIN InStocks I ON W.WarehouseID = I.WarehouseID AND P.ProductID = I.ProductID
    WHERE I.Quantity > 30
    ORDER BY W.WarehouseID, P.ProductID;

    -- Hoặc dùng EXISTS nếu chỉ cần biết có tồn tại bản ghi thỏa mãn
    SELECT A.*, B.*
    FROM Warehouses A, Products B
    WHERE EXISTS (SELECT 1
                  FROM InStocks I
                  WHERE I.WarehouseID = A.WarehouseID
                    AND I.ProductID = B.ProductID
                    AND I.Quantity > 30)
    ORDER BY A.WarehouseID, B.ProductID;
    ```

#### 📥 **4.18. Truy vấn con trong mệnh đề `FROM` (Subqueries in FROM Clauses)**
*   Subquery trong `FROM` được coi như một quan hệ (bảng tạm).
*   Subquery trong `FROM` phải được đặt trong dấu ngoặc đơn và **phải có một bí danh (alias)**.
*   **Ví dụ (slide 81):** Tìm thông tin sản phẩm được lưu trữ trong kho `WarehouseID = 'W01'`.
    ```sql
    SELECT A.*
    FROM Products A,
         (SELECT ProductID  -- Subquery tạo bảng tạm B chỉ chứa ProductID từ Instocks của kho W01
          FROM Instocks
          WHERE WarehouseID = 'W01') AS B -- B là alias cho subquery
    WHERE A.ProductID = B.ProductID;
    ```
    *Cách viết dùng `JOIN` thường hiệu quả và dễ đọc hơn:*
    ```sql
    SELECT P.*
    FROM Products P
    INNER JOIN Instocks I ON P.ProductID = I.ProductID
    WHERE I.WarehouseID = 'W01';
    ```

#### 🤝 **4.19. Biểu thức JOIN trong SQL (SQL Join Expressions)**
Cho `R1`, `R2` là các quan hệ, `P` là biểu thức điều kiện.
1.  **`CROSS JOIN` (Tích Đề-các):** `R1 × R2`
    *   Cú pháp: `FROM R1 CROSS JOIN R2` (hoặc `FROM R1, R2` - join ngầm)
2.  **`INNER JOIN` (Kết nối trong):**
    *   **`JOIN ... ON P`:** Kết nối dựa trên điều kiện `P`.
        *   Cú pháp: `FROM R1 [INNER] JOIN R2 ON P`
    *   **`Theta Join`:** Là một trường hợp của `JOIN ON P` khi `P` là một điều kiện so sánh tổng quát.
    *   **`NATURAL JOIN`:** Tự động kết nối trên các cột có cùng tên và kiểu dữ liệu.
        *   Cú pháp: `FROM R1 NATURAL JOIN R2`
        *   Tương đương: `FROM R1 JOIN R2 ON R1.X = R2.X` (nếu X là các cột chung, và X chỉ xuất hiện một lần trong kết quả).
3.  **`OUTER JOIN` (Kết nối ngoài):**
    *   **`LEFT OUTER JOIN`:** Giữ tất cả các hàng từ `R1`.
        *   `FROM R1 LEFT OUTER JOIN R2 ON P`
        *   `FROM R1 NATURAL LEFT OUTER JOIN R2`
    *   **`RIGHT OUTER JOIN`:** Giữ tất cả các hàng từ `R2`.
        *   `FROM R1 RIGHT OUTER JOIN R2 ON P`
        *   `FROM R1 NATURAL RIGHT OUTER JOIN R2`
    *   **`FULL OUTER JOIN`:** Giữ tất cả các hàng từ cả `R1` và `R2`.
        *   `FROM R1 FULL OUTER JOIN R2 ON P`
        *   `FROM R1 NATURAL FULL OUTER JOIN R2`
*   **Ví dụ `NATURAL LEFT OUTER JOIN` (slide 84):** Tìm thông tin khách hàng chưa bao giờ đặt hàng.
    ```sql
    SELECT A.*
    FROM Customers A
    NATURAL LEFT OUTER JOIN Orders B -- Giả sử Orders có CustomerID cùng tên với Customers
    WHERE B.OrderID IS NULL -- Nếu không có đơn hàng, các cột từ Orders (B) sẽ là NULL
    ORDER BY A.CustomerName;
    ```
    *Nếu không dùng `NATURAL` (khuyến khích hơn vì rõ ràng):*
    ```sql
    SELECT C.*
    FROM Customers C
    LEFT JOIN Orders O ON C.CustomerID = O.CustomerID
    WHERE O.OrderID IS NULL
    ORDER BY C.CustomerName;
    ```

#### 🚫 **4.20. Loại bỏ Trùng lặp (Eliminating Duplicates - `SELECT DISTINCT`)**
*   Hệ thống SQL (theo mặc định) không loại bỏ các bộ trùng lặp trong kết quả truy vấn.
*   Nếu muốn loại bỏ trùng lặp, sử dụng từ khóa `DISTINCT` sau `SELECT`.
    *   Cú pháp: `SELECT DISTINCT X ...`
*   Việc đặt `DISTINCT` sau mỗi `SELECT` không phải lúc nào cũng vô hại (có thể ảnh hưởng hiệu năng vì DBMS phải sắp xếp hoặc phân hoạch để tìm trùng lặp).

#### 📊 **4.21 & 4.22. Toán tử Gom nhóm và Tổng hợp (Grouping and Aggregation Operators)**
*   **Trong Đại số Quan hệ:** Hàm tổng hợp và phép Gom nhóm (𝒢).
*   **Trong SQL:**
    ```sql
    SELECT <Danh_sach_cot_gom_nhom> [, Ham_tong_hop1, Ham_tong_hop2, ...]
    FROM <Cac_bang>
    [WHERE <Dieu_kien_hang>]
    GROUP BY <Danh_sach_cot_de_gom_nhom>
    [HAVING <Dieu_kien_nhom>];
    ```
*   **Các hàm tổng hợp (Aggregation Operators - slide 87):**
    *   `SUM(cot)`: Tổng giá trị.
    *   `AVG(cot)`: Giá trị trung bình.
    *   `MIN(cot)`: Giá trị nhỏ nhất.
    *   `MAX(cot)`: Giá trị lớn nhất.
    *   `COUNT(cot)`: Đếm số lượng giá trị không `NULL`.
    *   `COUNT(*)`: Đếm tất cả các hàng trong nhóm (hoặc bảng nếu không có `GROUP BY`) thỏa mãn `WHERE`.
    *   `COUNT(DISTINCT cot)`: Đếm số lượng giá trị *duy nhất* không `NULL` của cột.

#### 🧩 **4.23. Gom nhóm (Grouping - `GROUP BY`)**
*   Sử dụng mệnh đề `GROUP BY` sau mệnh đề `WHERE` (nếu có).
*   **Lưu ý:**
    1.  `GROUP BY` được theo sau bởi danh sách các **thuộc tính gom nhóm (grouping attributes)**.
    2.  Bất kỳ hàm tổng hợp nào trong mệnh đề `SELECT` chỉ được áp dụng **bên trong các nhóm** đã được tạo.
    3.  Các cột trong mệnh đề `SELECT` phải là các thuộc tính gom nhóm hoặc kết quả của hàm tổng hợp.
*   **Ví dụ (slide 88):** Tìm tổng số lượng (`Quantity`) cho mỗi sản phẩm (`ProductID`) đã được đặt hàng.
    ```sql
    SELECT ProductID, SUM(Quantity)
    FROM OrderDetails
    GROUP BY ProductID;
    ```

#### ∅ **4.24. Gom nhóm, Tổng hợp và Giá trị NULL (Grouping, Aggregation, and Nulls)**
*   **NULL trong hàm tổng hợp:**
    *   Giá trị `NULL` bị **bỏ qua** trong hầu hết các hàm tổng hợp (`SUM`, `AVG`, `MIN`, `MAX`, `COUNT(cot)`). Nó không đóng góp vào tổng, trung bình, hoặc việc đếm giá trị của một thuộc tính, cũng không thể là min/max.
    *   `COUNT(*)` đếm tất cả các hàng, bao gồm cả hàng có giá trị `NULL`.
    *   `COUNT(cot)` chỉ đếm các hàng có giá trị `cot` không `NULL`.
*   **NULL trong gom nhóm (`GROUP BY`):**
    *   `NULL` được coi như một giá trị bình thường khi hình thành các nhóm. Có thể có một nhóm mà một hoặc nhiều thuộc tính gom nhóm có giá trị `NULL`.
*   **Kết quả tổng hợp trên nhóm rỗng:**
    *   Khi thực hiện bất kỳ hàm tổng hợp nào (trừ `COUNT`) trên một tập giá trị rỗng, kết quả là `NULL`.
    *   `COUNT` của một tập rỗng là `0`.
*   **Ví dụ (slide 90):**
    *   Hiển thị tổng chi phí đơn hàng cho mỗi khách hàng (ID và Tên).
        ```sql
        SELECT C.CustomerID, C.CustomerName,
               SUM(OD.Quantity * OD.UnitPrice * (1 - OD.Discount)) AS 'Total Cost' -- Giả sử Discount là tỉ lệ
        FROM Orders O
        JOIN OrderDetails OD ON O.OrderID = OD.OrderID
        JOIN Customers C ON O.CustomerID = C.CustomerID
        GROUP BY C.CustomerID, C.CustomerName;
        ```
    *   Hiển thị tổng chi phí cho mỗi đơn hàng trong năm 2018. (SQLite `strftime`)
        ```sql
        SELECT O.OrderID, SUM(OD.Quantity * OD.UnitPrice * (1 - OD.Discount)) AS 'Total Cost'
        FROM Orders O
        JOIN OrderDetails OD ON O.OrderID = OD.OrderID
        WHERE strftime('%Y', O.OrderDate) = '2018'
        GROUP BY O.OrderID;
        ```

####筛选 **4.25. Mệnh đề `HAVING` (HAVING Clauses)**
*   Điều kiện trong `WHERE` hạn chế các hàng *trước khi* gom nhóm.
*   Điều kiện trong `HAVING` hạn chế các *nhóm sau khi* đã gom nhóm.
*   **Ví dụ (slide 91):** In tổng chi phí đơn hàng chỉ cho những đơn hàng mà chi phí của *ít nhất một sản phẩm trong đơn hàng đó* (Min(Quantity * Price)) lớn hơn hoặc bằng 100. (Logic này hơi lạ, thường HAVING sẽ dùng với hàm tổng hợp trên cả nhóm, ví dụ `SUM(Quantity * Price) >= 1000`).
    *   Theo ví dụ slide:
    ```sql
    SELECT OrderID, SUM(Quantity * UnitPrice) AS 'Total Cost'
    FROM OrderDetails
    GROUP BY OrderID
    HAVING MIN(Quantity * UnitPrice) >= 100; -- Chỉ những nhóm (OrderID) mà giá trị nhỏ nhất của (Quantity * UnitPrice) trong nhóm đó >= 100
    ```
*   **Quy tắc cho `HAVING`:**
    *   Một hàm tổng hợp trong `HAVING` chỉ áp dụng cho các bộ của nhóm đang được kiểm tra.
    *   Bất kỳ thuộc tính nào của các quan hệ trong mệnh đề `FROM` đều có thể được tổng hợp trong `HAVING`.
    *   Các cột không phải là hàm tổng hợp trong `HAVING` phải là một phần của `GROUP BY`.

#### 👑 **4.26 & 4.27. Tìm Nhóm Lớn nhất (Finding Maximum Group)**
*   **Ví dụ (slide 92):** Tìm Đơn hàng (`OrderID`) có Tổng chi phí (`Total Cost`) là lớn nhất.
    *   Cách dùng `HAVING ... >= ALL (subquery)` (SQLite không hỗ trợ `ALL` với toán tử so sánh này trực tiếp trong `HAVING` theo cách này):
        ```sql
        -- Cú pháp lý thuyết, có thể không chạy trên mọi DBMS
        SELECT OrderID, SUM(Quantity * UnitPrice) AS TotalFree
        FROM OrderDetails
        GROUP BY OrderID
        HAVING TotalFree >= ALL (SELECT SUM(Quantity * UnitPrice)
                                 FROM OrderDetails
                                 GROUP BY OrderID);
        ```
    *   **Cách làm trong SQLite (và nhiều DBMS khác) (slide 93):** Dùng subquery lồng nhau.
        ```sql
        SELECT OrderID, SUM(Quantity * UnitPrice) AS TotalFree
        FROM OrderDetails
        GROUP BY OrderID
        HAVING TotalFree = (
            SELECT MAX(TotalCostSub) -- Lấy giá trị Max từ subquery bên trong
            FROM (
                SELECT SUM(Quantity * UnitPrice) AS TotalCostSub
                FROM OrderDetails
                GROUP BY OrderID
            ) AS SubQueryAlias -- Cần alias cho subquery trong FROM (nếu DBMS yêu cầu)
        );
        ```
        *Hoặc đơn giản hơn, dùng `ORDER BY` và `LIMIT` nếu chỉ cần một kết quả:*
        ```sql
        SELECT OrderID, SUM(Quantity * UnitPrice) AS TotalFree
        FROM OrderDetails
        GROUP BY OrderID
        ORDER BY TotalFree DESC
        LIMIT 1;
        ```
        *Nếu có nhiều đơn hàng cùng có tổng chi phí lớn nhất và muốn lấy tất cả, cách dùng subquery với `MAX` như slide 93 là phù hợp.*

---

### **PHẦN 5: RÀNG BUỘC TOÀN VẸN (INTEGRITY CONSTRAINTS)**

#### 🛡️ **5.1 & 5.2. Khái niệm và Thành phần Ràng buộc Toàn vẹn**
*   **Ràng buộc toàn vẹn (Integrity Constraint):** Là một quy tắc logic mà dữ liệu trong CSDL phải tuân theo để đảm bảo tính đúng đắn, nhất quán.
*   **Các thành phần của một ràng buộc:**
    1.  **Bối cảnh (Context):** Quan hệ (bảng) mà ràng buộc áp dụng.
        *   Ví dụ (slide 94): `R(A,B,C)`
    2.  **Điều kiện (Condition):** Phát biểu logic phải đúng.
        *   Ví dụ: `∀t ∈ r (t.B > t.C)` (Với mọi bộ `t` trong thể hiện `r` của `R`, giá trị của `B` phải lớn hơn giá trị của `C`).
    3.  **Bảng ảnh hưởng (Influence table):** Cho biết thao tác nào (Insert, Delete, Update) trên quan hệ có thể vi phạm ràng buộc.
        *   `+`: Thao tác có thể vi phạm.
        *   `-`: Thao tác không thể vi phạm.
        *   `+(X/Y)`: Update trên cột X hoặc Y có thể vi phạm.
        *   Ví dụ cho `R(A,B,C)` với `B > C`:
            | Thao tác | Ảnh hưởng |
            | :------- | :-------- |
            | Insert   | `+`       |
            | Delete   | `-`       |
            | Update   | `+(B/C)`  |
*   **Trigger (Bộ kích hoạt):**
    *   Khi một thao tác có dấu `+` trong bảng ảnh hưởng, ta có thể viết một **Trigger** để kiểm soát thao tác đó (ví dụ: ngăn chặn nếu vi phạm, hoặc thực hiện hành động khắc phục).
    *   Trigger là một hành động được định hướng bởi sự kiện, chạy tự động khi một thao tác thay đổi dữ liệu cụ thể (`INSERT`, `UPDATE`, `DELETE`) được thực hiện trên một bảng cụ thể.
    *   Hữu ích cho việc: thực thi quy tắc nghiệp vụ, xác thực dữ liệu đầu vào, lưu vết kiểm toán (audit trail).

#### ⚙️ **5.3. Trigger trong SQLite**
*   **Cú pháp tạo Trigger (slide 96):**
    ```sql
    CREATE TRIGGER [IF NOT EXISTS] ten_trigger
    [BEFORE | AFTER | INSTEAD OF] -- Thời điểm kích hoạt
    [INSERT | UPDATE [OF cot1, cot2,...] | DELETE] -- Sự kiện kích hoạt
    ON ten_bang
    [FOR EACH ROW] -- (Thường ngầm định nếu không có WHEN tổng quát)
    [WHEN dieu_kien_trigger] -- Điều kiện để trigger chạy
    BEGIN
        -- Các câu lệnh SQL thực thi khi trigger được kích hoạt;
        -- Ví dụ: SELECT CASE WHEN ... THEN RAISE(ABORT, 'Thông báo lỗi') END;
    END;
    ```
*   **Xóa Trigger:**
    ```sql
    DROP TRIGGER [IF EXISTS] ten_trigger;
    ```
*   **Truy cập dữ liệu hàng (slide 97):**
    *   `OLD.ten_cot`: Giá trị của cột *trước khi* có sự thay đổi (trong `UPDATE`, `DELETE`).
    *   `NEW.ten_cot`: Giá trị của cột *sau khi* có sự thay đổi (trong `INSERT`, `UPDATE`).
    *   **Khả dụng:**
        *   `INSERT`: Chỉ `NEW` khả dụng.
        *   `UPDATE`: Cả `OLD` và `NEW` đều khả dụng.
        *   `DELETE`: Chỉ `OLD` khả dụng.
*   **Ví dụ (slide 98-99):** Xác thực địa chỉ email trước khi chèn khách hàng mới.
    ```sql
    CREATE TRIGGER validateEmailCustomer
    BEFORE INSERT ON Customer
    FOR EACH ROW -- Cần thiết để tham chiếu NEW.email
    BEGIN
        SELECT CASE
            WHEN NEW.email NOT LIKE '%_@__%.__%' THEN -- Kiểm tra mẫu email cơ bản
                RAISE(ABORT, 'Invalid email address')
        END;
    END;
    ```
    *   Khi `INSERT` một bộ, nếu email không hợp lệ, hàm `RAISE(ABORT, ...)` sẽ hủy bỏ việc chèn và đưa ra thông báo lỗi.

#### ✅ **5.4 & 5.5. Các Ràng buộc Toàn vẹn Phổ biến trong SQL (Common Integrity Constraints)**
*   Ràng buộc là các quy tắc được thực thi trên các cột dữ liệu của bảng.
*   Có thể ở **cấp độ cột (column level)** hoặc **cấp độ bảng (table level)**.
    *   Ràng buộc cấp cột chỉ áp dụng cho một cột.
    *   Ràng buộc cấp bảng áp dụng cho toàn bộ bảng (có thể liên quan đến nhiều cột).
*   **Cú pháp trong `CREATE TABLE` (slide 100):**
    ```sql
    CREATE TABLE ten_bang (
        cot1 kieu_du_lieu [rang_buoc_cot],
        cot2 kieu_du_lieu [rang_buoc_cot],
        ...,
        [CONSTRAINT ten_rang_buoc_bang] <Dinh_nghia_rang_buoc_bang>
    );
    ```
*   **Các ràng buộc phổ biến trong SQLite (slide 101):**
    1.  **`NOT NULL`:** Đảm bảo cột không thể có giá trị `NULL`. (Cấp cột)
        *   **Ví dụ (slide 103):**
            ```sql
            CREATE TABLE Products (
                ProductID TEXT PRIMARY KEY,
                ProductName TEXT NOT NULL,
                UnitPrice REAL NOT NULL,
                CategoryID TEXT NOT NULL
            );
            ```
    2.  **`DEFAULT gia_tri`:** Cung cấp giá trị mặc định cho cột khi không có giá trị nào được chỉ định lúc chèn. (Cấp cột)
        *   **Ví dụ (slide 104):**
            ```sql
            CREATE TABLE Orders (
                OrderID TEXT PRIMARY KEY,
                OrderDate TEXT DEFAULT CURRENT_DATE, -- CURRENT_DATE: ngày hiện tại
                RequiredDate TEXT NOT NULL,
                CustomerID TEXT
            );
            -- Khi chèn bỏ qua OrderDate, nó sẽ lấy ngày hiện tại.
            INSERT INTO Orders (OrderID, RequiredDate, CustomerID)
            VALUES ('O01', '2018-10-22', 'C01');
            -- SELECT * FROM Orders; -> ('O01', '2018-10-20', '2018-10-22', 'C01') (giả sử ngày hiện tại là 2018-10-20)
            ```
    3.  **`UNIQUE`:** Đảm bảo tất cả các giá trị trong một cột (hoặc tổ hợp cột) là khác nhau. (Cấp cột hoặc bảng)
        *   **Ví dụ (slide 105):**
            ```sql
            CREATE TABLE Categories (
                CategoryID TEXT PRIMARY KEY,
                CategoryName TEXT NOT NULL UNIQUE, -- Ràng buộc UNIQUE cấp cột
                Description TEXT -- Sửa từ Deacription
            );
            ```
    4.  **`PRIMARY KEY`:** Định danh duy nhất mỗi hàng/bản ghi trong bảng CSDL. Ngầm định là `UNIQUE` và `NOT NULL`. (Cấp cột hoặc bảng)
    5.  **`CHECK (dieu_kien)`:** Đảm bảo tất cả các giá trị trong một cột (hoặc các giá trị trong hàng ở cấp bảng) thỏa mãn một điều kiện nhất định. (Cấp cột hoặc bảng)
        *   **Cú pháp (slide 106):**
            *   Cấp cột: `columnName dataType CHECK(expression)`
            *   Cấp bảng: `CONSTRAINT constraintName CHECK(expression)`
        *   **Ví dụ (slide 107 - Ràng buộc bảng):** Đảm bảo `RequiredDate` không sớm hơn `OrderDate`.
            ```sql
            CREATE TABLE Orders (
                OrderID TEXT PRIMARY KEY,
                OrderDate TEXT DEFAULT CURRENT_DATE,
                RequireDate TEXT NOT NULL, -- Sửa từ RequireDate
                CustomerID TEXT,
                CONSTRAINT ValidateRequireDate CHECK (strftime('%Y-%m-%d', RequireDate) >= strftime('%Y-%m-%d', OrderDate)) -- So sánh ngày tháng
            );
            -- Lưu ý: slide dùng strftime('%d',...) so sánh ngày trong tháng, có thể không đúng ý đồ.
            -- Nên so sánh toàn bộ ngày tháng. SQLite so sánh chuỗi ngày dạng YYYY-MM-DD đúng.
            ```

#### 🔗 **5.7 & 5.8. Ràng buộc Khóa Ngoại trong SQL (SQL Foreign Key Constraints)**
*   **Khóa ngoại (Foreign Key):** Trong một quan hệ, một hoặc nhiều thuộc tính được gọi là khóa ngoại nếu chúng không phải là khóa (chính) trong quan hệ này, nhưng là khóa chính trong một quan hệ khác.
*   Khóa ngoại khẳng định rằng một giá trị xuất hiện trong một quan hệ cũng phải xuất hiện trong thành phần khóa chính của một quan hệ khác (hoặc là `NULL` nếu được phép).
*   **Ví dụ (slide 108):**
    *   `Class(ClassID, Description)` (ClassID là PK)
    *   `Student(StudentID, Name, ..., ClassID)` (ClassID ở đây là FK tham chiếu đến `Class.ClassID`)
        *   Nếu `Class` có `C01, C02`. `Student` có thể có `ClassID` là `C01, C02` nhưng không thể là `C03` (trừ khi `C03` tồn tại trong `Class`).
*   **Khai báo Ràng buộc Khóa Ngoại (slide 109-110):**
    1.  **Điều kiện tham chiếu:** Thuộc tính (hoặc tập thuộc tính) `X` của quan hệ được tham chiếu (`R1`) phải được khai báo là `UNIQUE` hoặc `PRIMARY KEY`.
    2.  **Toàn vẹn tham chiếu:** `π_X(R2) ⊆ π_X(R1)` (Mọi giá trị khóa ngoại trong `R2` phải tồn tại trong tập giá trị khóa chính/duy nhất của `R1`, hoặc là `NULL`).
    3.  **Chính sách khi Update/Delete ở bảng được tham chiếu (`R1`):**
        *   **`Default (NO ACTION / RESTRICT)`:** Từ chối các sửa đổi vi phạm (ví dụ: không cho xóa hàng ở `R1` nếu có hàng ở `R2` tham chiếu đến nó). SQLite `NO ACTION` trì hoãn kiểm tra đến cuối giao dịch, `RESTRICT` kiểm tra ngay.
        *   **`CASCADE`:** Khi thay đổi (update khóa chính, delete hàng) ở `R1`, thay đổi tương ứng được lan truyền sang các hàng tham chiếu ở `R2`.
            *   `ON UPDATE CASCADE`: Nếu PK ở `R1` thay đổi, FK ở `R2` cũng thay đổi theo.
            *   `ON DELETE CASCADE`: Nếu hàng ở `R1` bị xóa, các hàng tham chiếu ở `R2` cũng bị xóa.
        *   **`SET NULL`:** Khi thay đổi ở `R1` ảnh hưởng đến giá trị khóa ngoại ở `R2`, giá trị khóa ngoại đó ở `R2` được đặt thành `NULL` (cột FK phải cho phép `NULL`).
        *   **`SET DEFAULT`:** Tương tự `SET NULL` nhưng đặt thành giá trị mặc định của cột FK.
        *   *Khai báo thường dùng: `ON UPDATE CASCADE`, `ON DELETE SET NULL` (hoặc `CASCADE` tùy logic).*
*   **Cú pháp khai báo FK (slide 111):**
    ```sql
    -- Cấp cột
    CREATE TABLE R2 (
        Z kieu_du_lieu,
        X kieu_du_lieu REFERENCES R1(X_cua_R1)
            [ON UPDATE hanh_dong] [ON DELETE hanh_dong]
    );

    -- Cấp bảng
    CREATE TABLE R2 (
        Z kieu_du_lieu,
        X kieu_du_lieu,
        ...,
        FOREIGN KEY (X) REFERENCES R1(X_cua_R1)
            [ON UPDATE hanh_dong] [ON DELETE hanh_dong]
    );
    ```
*   **Ví dụ (slide 111):** `ShipperDetail`
    ```sql
    CREATE TABLE ShipperDetail (
        ShipperID TEXT,
        ProductID TEXT,
        Quantity INT,
        PRIMARY KEY (ShipperID, ProductID),
        FOREIGN KEY (ShipperID) REFERENCES Shippers(ShipperID) -- Giả sử bảng Shippers có PK là ShipperID
            ON DELETE SET NULL ON UPDATE CASCADE,
        FOREIGN KEY (ProductID) REFERENCES Products(ProductID) -- Giả sử bảng Products có PK là ProductID
            ON DELETE SET NULL ON UPDATE CASCADE -- Slide ghi Products(ShipperID) có thể là lỗi, phải là ProductID
    );
    ```
    *Lưu ý: SQLite yêu cầu bật hỗ trợ khóa ngoại bằng `PRAGMA foreign_keys = ON;` cho mỗi kết nối.*

---

### **PHẦN 6: KHUNG NHÌN VÀ CHỈ MỤC (VIEWS AND INDEX)**

#### 🖼️ **6.9 & Views (slide 112-113): Khung nhìn (Views)**
*   `CREATE TABLE` tạo bảng trong CSDL, lưu trữ vật lý.
*   **Khung nhìn (View)** là một loại quan hệ SQL khác, không tồn tại vật lý (còn gọi là bảng ảo - virtual table). Chúng được định nghĩa bởi một biểu thức giống như một câu truy vấn.
*   View có thể được truy vấn như thể chúng tồn tại vật lý. Trong một số trường hợp, có thể sửa đổi view (chèn, cập nhật, xóa) và thay đổi sẽ ảnh hưởng đến bảng cơ sở.
*   **Trong SQLite (theo slide):** View không cho phép thực hiện các thao tác `INSERT`, `UPDATE`, `DELETE` trực tiếp trên view. (Một số DBMS khác có thể cho phép nếu view đủ đơn giản và có thể cập nhật được). *Tuy nhiên, SQLite mới hơn có hỗ trợ `INSTEAD OF TRIGGER` trên view để thực hiện các hành động này.*
*   **Cú pháp tạo View:**
    ```sql
    CREATE VIEW ten_view AS
    SELECT cot1, cot2, ...
    FROM ten_bang
    [WHERE dieu_kien];
    ```
*   **Xóa View:**
    ```sql
    DROP VIEW ten_view;
    ```
*   **Ví dụ (slide 113):** Tạo view cho khách hàng với tổng giá trị đơn hàng.
    ```sql
    CREATE VIEW CustomerTotalOrder AS
    SELECT O.CustomerID, SUM(OD.UnitPrice * OD.Quantity * (1 - OD.Discount)) AS Total
    FROM Orders O
    JOIN OrderDetail OD ON O.OrderID = OD.OrderID -- Sửa tên bảng thành OrderDetail (nếu đó là tên đúng)
    GROUP BY O.CustomerID;
    ```

#### 🔍 **6.10. Truy vấn Khung nhìn (Querying Views)**
*   View có thể được truy vấn chính xác như một bảng đã lưu trữ.
*   **Ví dụ (slide 114):** Tìm thông tin khách hàng cùng với tổng đơn hàng của họ.
    ```sql
    SELECT C.*, CTO.Total
    FROM Customers C, CustomerTotalOrder CTO -- CustomerTotalOrder là view đã tạo
    WHERE C.CustomerID = CTO.CustomerID;
    ```
*   **Mở rộng View (View Expansion - slide 115):** DBMS có thể thay thế mỗi view trong mệnh đề `FROM` bằng định nghĩa subquery của view đó.
    ```sql
    SELECT C.*, Sub.Total
    FROM Customers C,
         (SELECT O.CustomerID, SUM(OD.UnitPrice * OD.Quantity * (1 - OD.Discount)) AS Total
          FROM Orders O JOIN OrderDetail OD ON O.OrderID = OD.OrderID
          GROUP BY O.CustomerID) AS Sub -- Subquery này chính là định nghĩa của CustomerTotalOrder
    WHERE C.CustomerID = Sub.CustomerID;
    ```

#### 📛 **6.11. Đổi tên Thuộc tính trong View (Renaming Attributes in Views)**
*   Có thể đặt tên mới cho các thuộc tính của view.
*   **Cú pháp:**
    ```sql
    CREATE VIEW ten_view (ten_cot_moi1, ten_cot_moi2, ...) AS
    SELECT bieu_thuc_cot1, bieu_thuc_cot2, ...
    FROM ...;
    ```
*   **Ví dụ (slide 116):**
    ```sql
    CREATE VIEW ProductInstock (Product, TotalQuantity) AS
    SELECT ProductID, SUM(Quantity)
    FROM Instocks
    GROUP BY ProductID;
    ```
*   **Lưu ý (slide 116):** View có thể được sửa đổi (insert, delete, update) bằng các câu lệnh SQL, nhưng điều này liên quan đến một số điều kiện phức tạp (confuse conditions). Tài liệu không trình bày ở đây. (Ví dụ: view phải dựa trên một bảng duy nhất, không có `GROUP BY`, `DISTINCT`, hàm tổng hợp, và phải bao gồm khóa chính của bảng cơ sở để có thể cập nhật).

#### 🚀 **6.12. Chỉ mục là gì? (What is an index?)**
*   Mỗi hàng trong bảng (trong SQLite) có một `rowID` (số thứ tự) để định danh hàng đó. (Nếu bảng có `INTEGER PRIMARY KEY`, cột đó chính là `rowID`).
*   Do đó, có thể xem bảng như một danh sách các cặp: `rowID` và một hoặc nhiều **cột** mà ta muốn sắp xếp giá trị; đây được gọi là **bảng chỉ mục (Index table)**.
*   **Chỉ mục (Index)** là một cấu trúc dữ liệu bổ sung giúp tăng tốc độ truy vấn, kết nối (`JOIN`), và các thao tác gom nhóm (`GROUP BY`).
*   **Nhược điểm:** Chỉ mục làm **chậm quá trình nhập liệu** (`INSERT`, `UPDATE`, `DELETE`) vì chỉ mục cũng cần được cập nhật.
*   Chỉ mục có thể được tạo hoặc xóa mà **không ảnh hưởng đến dữ liệu** trong bảng.

#### 🏗️ **6.13. Tạo và Xóa Chỉ mục (Create & Drop Indexes)**
*   **Tạo chỉ mục trên một cột:**
    ```sql
    CREATE INDEX ten_chi_muc ON ten_bang (ten_cot [ASC | DESC]);
    ```
*   **Tạo chỉ mục trên nhiều cột (composite index):**
    ```sql
    CREATE INDEX ten_chi_muc ON ten_bang (cot1 [ASC | DESC], cot2 [ASC | DESC], ...);
    ```
*   **Tạo chỉ mục duy nhất (giá trị trong cột/tổ hợp cột phải là duy nhất):**
    ```sql
    CREATE UNIQUE INDEX ten_chi_muc ON ten_bang (ten_cot);
    ```
*   **Xóa chỉ mục:**
    ```sql
    DROP INDEX ten_chi_muc;
    ```
*   **Ví dụ (slide 119):**
    *   Bảng `Categories`:
        | rowID | CategoryID | CategoryName | Description |
        | :---- | :--------- | :----------- | :---------- |
        | 1     | c1         | Rice         | ...         |
        | 2     | c2         | Electronic   | ...         |
        | 3     | c3         | Flower       | ...         |
    *   Tạo chỉ mục:
        ```sql
        CREATE INDEX CategoryNameIndex ON Categories(CategoryName ASC);
        ```
    *   Cấu trúc chỉ mục (logic):
        | CategoryName | rowID |
        | :----------- | :---- |
        | Electronic   | 2     |
        | Flower       | 3     |
        | Rice         | 1     |
        *(Chỉ mục được sắp xếp theo `CategoryName`)*

#### 🤔 **6.14. Khi nào nên tạo chỉ mục? (When should indexes be created)**
*   Một cột chứa một **phạm vi giá trị rộng** (nhiều giá trị khác nhau, tính chọn lọc cao).
*   Một cột **không chứa một số lượng lớn giá trị `NULL`**.
*   Một hoặc nhiều cột thường xuyên được sử dụng cùng nhau trong mệnh đề `WHERE` hoặc điều kiện `JOIN`.

#### 🤷 **6.15. Khi nào nên tránh tạo chỉ mục? (When should indexes be avoided)**
*   **Bảng nhỏ:** Lợi ích về tốc độ truy vấn không đáng kể so với chi phí quét toàn bộ bảng.
*   Các cột **không thường xuyên được sử dụng làm điều kiện** trong truy vấn.
*   Cột được **cập nhật thường xuyên:** Chi phí duy trì chỉ mục cao.

---
