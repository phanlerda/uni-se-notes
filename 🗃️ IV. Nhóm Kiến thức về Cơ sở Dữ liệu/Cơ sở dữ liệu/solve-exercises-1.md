
---

## 📝 **BÀI TẬP: QUẢN LÝ SINH VIÊN (STUDENT MANAGEMENT DATABASE - SMDB)** 📝

---

### **I. MÔ TẢ CƠ SỞ DỮ LIỆU**

Dựa trên mô tả trong tài liệu:

1.  **Subject (Môn học)**
    *   Thuộc tính: `SubjectID`, `SubjectName`, `Units`
    *   Mô tả: Mỗi môn học có một mã (`SubjectID`) duy nhất, tên môn học (`SubjectName`) và số tín chỉ (`Units`).
    *   **Lược đồ:** `Subject (SubjectID, SubjectName, Units)`

2.  **Class (Lớp học)**
    *   Thuộc tính: `ClassID`, `ClassName`, `ClassYear`
    *   Mô tả: Mỗi lớp học có một mã (`ClassID`) duy nhất, tên lớp (`ClassName`) và năm học (`ClassYear`).
    *   **Lược đồ:** `Class (ClassID, ClassName, ClassYear)`

3.  **Student (Sinh viên)**
    *   Thuộc tính: `StudentID`, `StudentName`, `StudentAddress`, `ClassID`
    *   Mô tả: Mỗi sinh viên có một mã (`StudentID`) duy nhất, tên (`StudentName`), địa chỉ (`StudentAddress`) và mã lớp học (`ClassID`) mà sinh viên đó thuộc về.
    *   **Lược đồ:** `Student (StudentID, StudentName, StudentAddress, ClassID)`

4.  **StudentGrades (Điểm của Sinh viên)**
    *   Thuộc tính: `StudentID`, `SubjectID`, `Grades`
    *   Mô tả: Lưu trữ điểm (`Grades`) của môn học (`SubjectID`) cho sinh viên (`StudentID`).
    *   **Lược đồ:** `StudentGrades (StudentID, SubjectID, Grades)`

---

### **II. YÊU CẦU (REQUIREMENTS)**

#### **1. Xác định tất cả các khóa của các Lược đồ Quan hệ (Determine all the keys of the Relational Schemes)**

*   **`Subject (SubjectID, SubjectName, Units)`**
    *   **Khóa chính (Primary Key):** `SubjectID` (vì mỗi môn học có mã duy nhất).
    *   *Khóa ứng viên (Candidate Key) có thể có:* Nếu `SubjectName` cũng là duy nhất, thì `SubjectName` cũng là một khóa ứng viên. Tuy nhiên, dựa trên mô tả, `SubjectID` là lựa chọn rõ ràng nhất cho khóa chính.

*   **`Class (ClassID, ClassName, ClassYear)`**
    *   **Khóa chính (Primary Key):** `ClassID` (vì mỗi lớp có mã duy nhất).
    *   *Khóa ứng viên có thể có:* Nếu tổ hợp `(ClassName, ClassYear)` là duy nhất (ví dụ: không thể có hai lớp "Công nghệ Thông tin K60" trong cùng một năm), thì `(ClassName, ClassYear)` cũng là một khóa ứng viên.

*   **`Student (StudentID, StudentName, StudentAddress, ClassID)`**
    *   **Khóa chính (Primary Key):** `StudentID` (vì mỗi sinh viên có mã duy nhất).
    *   **Khóa ngoại (Foreign Key):** `ClassID` tham chiếu đến `Class(ClassID)`.

*   **`StudentGrades (StudentID, SubjectID, Grades)`**
    *   **Khóa chính (Primary Key):** `(StudentID, SubjectID)` (một sinh viên chỉ có một điểm cho một môn học cụ thể).
    *   **Khóa ngoại (Foreign Keys):**
        *   `StudentID` tham chiếu đến `Student(StudentID)`.
        *   `SubjectID` tham chiếu đến `Subject(SubjectID)`.

#### **2. Tạo cơ sở dữ liệu SMDB (Create database SMDB)**

Bước này phụ thuộc vào Hệ Quản trị CSDL bạn sử dụng (ví dụ: SQLite, MySQL, PostgreSQL).
*   **SQLite:**
    *   Bạn có thể tạo một file CSDL mới bằng SQLite Browser hoặc từ dòng lệnh: `sqlite3 SMDB.db`
*   **MySQL/PostgreSQL:**
    *   Sử dụng lệnh: `CREATE DATABASE SMDB;`

#### **3. Tạo các Lược đồ Quan hệ (Create the Relational Schemes)**

Sử dụng lệnh `CREATE TABLE` trong SQL.

```sql
-- Bảng Subject
CREATE TABLE Subject (
    SubjectID CHAR(5) PRIMARY KEY,      -- Ví dụ: S01
    SubjectName VARCHAR(255) NOT NULL,
    Units INT NOT NULL CHECK (Units > 0) -- Số tín chỉ phải dương
);

-- Bảng Class
CREATE TABLE Class (
    ClassID CHAR(5) PRIMARY KEY,        -- Ví dụ: C01
    ClassName VARCHAR(255) NOT NULL,
    ClassYear VARCHAR(10) NOT NULL      -- Ví dụ: 2020-2024
);

-- Bảng Student
CREATE TABLE Student (
    StudentID CHAR(5) PRIMARY KEY,      -- Ví dụ: T01
    StudentName VARCHAR(255) NOT NULL,
    StudentAddress TEXT,
    ClassID CHAR(5) NOT NULL,
    FOREIGN KEY (ClassID) REFERENCES Class(ClassID)
        ON UPDATE CASCADE
        ON DELETE RESTRICT -- Hoặc SET NULL nếu logic cho phép sinh viên không thuộc lớp nào
);

-- Bảng StudentGrades
CREATE TABLE StudentGrades (
    StudentID CHAR(5) NOT NULL,
    SubjectID CHAR(5) NOT NULL,
    Grades REAL CHECK (Grades >= 0 AND Grades <= 10), -- Giả sử điểm theo thang 10
    PRIMARY KEY (StudentID, SubjectID),
    FOREIGN KEY (StudentID) REFERENCES Student(StudentID)
        ON UPDATE CASCADE
        ON DELETE CASCADE, -- Nếu xóa sinh viên thì xóa luôn điểm
    FOREIGN KEY (SubjectID) REFERENCES Subject(SubjectID)
        ON UPDATE CASCADE
        ON DELETE RESTRICT -- Không cho xóa môn học nếu có sinh viên đã có điểm môn đó
);
```

#### **4. Chèn dữ liệu (Insert data)**

Dựa trên yêu cầu:
*   `SubjectID`: S01 → S05
*   `ClassID`: C01 → C03
*   `StudentID`: T01 → T20
*   `StudentGrades`: Phân phối điểm của các môn cho sinh viên. 1-3 môn/sinh viên. Chỉ một nửa số sinh viên có điểm.

```sql
-- Chèn dữ liệu cho bảng Subject
INSERT INTO Subject (SubjectID, SubjectName, Units) VALUES
('S01', 'Cơ sở dữ liệu', 3),
('S02', 'Lập trình Python', 3),
('S03', 'Cấu trúc dữ liệu', 4),
('S04', 'Toán rời rạc', 3),
('S05', 'Mạng máy tính', 4);

-- Chèn dữ liệu cho bảng Class
INSERT INTO Class (ClassID, ClassName, ClassYear) VALUES
('C01', 'Công nghệ Thông tin K60', '2020-2024'),
('C02', 'Khoa học Máy tính K61', '2021-2025'),
('C03', 'Kỹ thuật Phần mềm K60', '2020-2024');

-- Chèn dữ liệu cho bảng Student (20 sinh viên)
-- Lớp C01 (7 SV)
INSERT INTO Student (StudentID, StudentName, StudentAddress, ClassID) VALUES
('T01', 'Nguyễn Văn An', '123 Đường A, Quận 1, TP.HCM', 'C01'),
('T02', 'Trần Thị Bình', '456 Đường B, Quận 2, TP.HCM', 'C01'),
('T03', 'Lê Văn Cường', '789 Đường C, Quận 3, TP.HCM', 'C01'),
('T04', 'Phạm Thị Dung', '101 Đường D, Quận 4, TP.HCM', 'C01'),
('T05', 'Hoàng Văn Em', '112 Đường E, Quận 5, TP.HCM', 'C01'),
('T06', 'Vũ Thị F', '213 Đường F, Quận 6, TP.HCM', 'C01'),
('T07', 'Đỗ Văn Giang', '314 Đường G, Quận 7, TP.HCM', 'C01');

-- Lớp C02 (7 SV)
INSERT INTO Student (StudentID, StudentName, StudentAddress, ClassID) VALUES
('T08', 'Ngô Thị Hạnh', '415 Đường H, Quận 8, TP.HCM', 'C02'),
('T09', 'Lý Văn Ích', '516 Đường I, Quận 9, TP.HCM', 'C02'),
('T10', 'Mai Thị Kim', '617 Đường K, Quận 10, TP.HCM', 'C02'),
('T11', 'Trịnh Văn Long', '718 Đường L, Quận 11, TP.HCM', 'C02'),
('T12', 'Bùi Thị Mai', '819 Đường M, Quận 12, TP.HCM', 'C02'),
('T13', 'Dương Văn Nam', '920 Đường N, Bình Thạnh, TP.HCM', 'C02'),
('T14', 'Hà Thị Oanh', '121 Đường O, Phú Nhuận, TP.HCM', 'C02');

-- Lớp C03 (6 SV)
INSERT INTO Student (StudentID, StudentName, StudentAddress, ClassID) VALUES
('T15', 'Kiều Văn Phúc', '222 Đường P, Gò Vấp, TP.HCM', 'C03'),
('T16', 'Ông Thị Quyên', '333 Đường Q, Tân Bình, TP.HCM', 'C03'),
('T17', 'Nông Văn Rèn', '444 Đường R, Tân Phú, TP.HCM', 'C03'),
('T18', 'Châu Thị Sương', '555 Đường S, Bình Tân, TP.HCM', 'C03'),
('T19', 'Ưng Văn Tài', '666 Đường T, Thủ Đức, TP.HCM', 'C03'),
('T20', 'Xoài Thị Út', '777 Đường U, Hóc Môn, TP.HCM', 'C03');


-- Chèn dữ liệu cho bảng StudentGrades (chỉ 10/20 sinh viên có điểm, 1-3 môn/SV)
-- SV T01
INSERT INTO StudentGrades (StudentID, SubjectID, Grades) VALUES
('T01', 'S01', 8.5),
('T01', 'S02', 7.0);
-- SV T02
INSERT INTO StudentGrades (StudentID, SubjectID, Grades) VALUES
('T02', 'S01', 9.0),
('T02', 'S03', 8.0),
('T02', 'S04', 7.5);
-- SV T03
INSERT INTO StudentGrades (StudentID, SubjectID, Grades) VALUES
('T03', 'S02', 6.5);
-- SV T04
INSERT INTO StudentGrades (StudentID, SubjectID, Grades) VALUES
('T04', 'S05', 9.5),
('T04', 'S01', 8.0);
-- SV T05
INSERT INTO StudentGrades (StudentID, SubjectID, Grades) VALUES
('T05', 'S03', 7.0),
('T05', 'S04', 8.5),
('T05', 'S05', 6.0);
-- SV T08
INSERT INTO StudentGrades (StudentID, SubjectID, Grades) VALUES
('T08', 'S01', 7.5);
-- SV T10
INSERT INTO StudentGrades (StudentID, SubjectID, Grades) VALUES
('T10', 'S02', 8.0),
('T10', 'S03', 9.0);
-- SV T12
INSERT INTO StudentGrades (StudentID, SubjectID, Grades) VALUES
('T12', 'S04', 6.0),
('T12', 'S05', 7.5);
-- SV T15
INSERT INTO StudentGrades (StudentID, SubjectID, Grades) VALUES
('T15', 'S01', 9.0);
-- SV T18
INSERT INTO StudentGrades (StudentID, SubjectID, Grades) VALUES
('T18', 'S02', 7.0),
('T18', 'S03', 8.5),
('T18', 'S05', 7.0);
```

#### **5. Truy vấn bằng Đại số Quan hệ và SQL (Query by Relational Algebra and SQL)**

##### **5.1. Hiển thị sinh viên của lớp có mã (ClassID) = "C02".**
*   **Đại số Quan hệ:**
    `π_{StudentID, StudentName, StudentAddress} (σ_{ClassID='C02'} (Student))`
    Hoặc nếu muốn tất cả thông tin: `σ_{ClassID='C02'} (Student)`
*   **SQL:**
    ```sql
    SELECT StudentID, StudentName, StudentAddress
    FROM Student
    WHERE ClassID = 'C02';

    -- Hoặc tất cả thông tin
    SELECT *
    FROM Student
    WHERE ClassID = 'C02';
    ```

##### **5.2. Hiển thị sinh viên của lớp có tên (ClassName) = "Computer Science".**
*   **Đại số Quan hệ:**
    `π_{StudentID, StudentName, StudentAddress} ( (σ_{ClassName='Khoa học Máy tính K61'} (Class)) ⋈ Student )`
    *(Giả sử "Computer Science" tương ứng với "Khoa học Máy tính K61")*
*   **SQL:**
    ```sql
    SELECT S.StudentID, S.StudentName, S.StudentAddress
    FROM Student S
    JOIN Class C ON S.ClassID = C.ClassID
    WHERE C.ClassName = 'Khoa học Máy tính K61';
    ```

##### **5.3. Hiển thị sinh viên (tất cả thông tin) của lớp có năm học (ClassYear) = "2020-2024".**
*   **Đại số Quan hệ:**
    ` (σ_{ClassYear='2020-2024'} (Class)) ⋈ Student `
*   **SQL:**
    ```sql
    SELECT S.*
    FROM Student S
    JOIN Class C ON S.ClassID = C.ClassID
    WHERE C.ClassYear = '2020-2024';
    ```

##### **5.4. Hiển thị tên môn học (SubjectName) và số tín chỉ (Units) của môn có mã (SubjectID) = “S01”.**
*   **Đại số Quan hệ:**
    `π_{SubjectName, Units} (σ_{SubjectID='S01'} (Subject))`
*   **SQL:**
    ```sql
    SELECT SubjectName, Units
    FROM Subject
    WHERE SubjectID = 'S01';
    ```

##### **5.5. Điểm (Grades) của môn có mã (SubjectID) = "S02" của sinh viên có mã (StudentID) = "T02".**
*   **Đại số Quan hệ:**
    `π_{Grades} (σ_{SubjectID='S02' AND StudentID='T02'} (StudentGrades))`
*   **SQL:**
    ```sql
    SELECT Grades
    FROM StudentGrades
    WHERE SubjectID = 'S02' AND StudentID = 'T02';
    ```

##### **5.6. Tìm Môn học (ID, Tên và Điểm) mà sinh viên có mã (StudentID) = "T02" bị rớt.**
*(Giả sử điểm rớt là < 5.0)*
*   **Đại số Quan hệ:**
    `π_{SG.SubjectID, S.SubjectName, SG.Grades} ( (σ_{SG.StudentID='T02' AND SG.Grades < 5.0} (StudentGrades { AS SG})) ⋈ Subject {AS S} )`
    *(Trong đó phép ⋈ là natural join trên SubjectID)*
*   **SQL:**
    ```sql
    SELECT SG.SubjectID, Sub.SubjectName, SG.Grades
    FROM StudentGrades SG
    JOIN Subject Sub ON SG.SubjectID = Sub.SubjectID
    WHERE SG.StudentID = 'T02' AND SG.Grades < 5.0;
    ```

##### **5.7. Hiển thị tất cả Môn học (\*) mà sinh viên có mã (StudentID) = "T03" chưa bao giờ thi (chưa có điểm).**
*   **Đại số Quan hệ:**
    `(π_{SubjectID} (Subject)) - (π_{SubjectID} (σ_{StudentID='T03'} (StudentGrades)))`
    Sau đó kết quả này (chỉ có SubjectID) được join với bảng Subject để lấy đầy đủ thông tin.
    `ResultIDs ← (π_{SubjectID} (Subject)) - (π_{SubjectID} (σ_{StudentID='T03'} (StudentGrades)))`
    `ResultIDs ⋈ Subject`
*   **SQL:**
    ```sql
    SELECT S.*
    FROM Subject S
    WHERE S.SubjectID NOT IN (SELECT SG.SubjectID
                              FROM StudentGrades SG
                              WHERE SG.StudentID = 'T03');
    -- Hoặc dùng LEFT JOIN
    SELECT S.*
    FROM Subject S
    LEFT JOIN StudentGrades SG ON S.SubjectID = SG.SubjectID AND SG.StudentID = 'T03'
    WHERE SG.Grades IS NULL; -- Hoặc SG.StudentID IS NULL (nếu join chỉ dựa trên SubjectID)
    ```

##### **5.8. Số lượng sinh viên của mỗi lớp.**
*   **Đại số Quan hệ:**
    `ClassID 𝒢_{COUNT(StudentID) \text{ AS NumberOfStudents}} (Student)`
    Kết quả join với bảng Class để lấy tên lớp nếu cần.
*   **SQL:**
    ```sql
    SELECT C.ClassID, C.ClassName, COUNT(S.StudentID) AS NumberOfStudents
    FROM Class C
    LEFT JOIN Student S ON C.ClassID = S.ClassID -- Dùng LEFT JOIN để hiển thị cả lớp không có SV
    GROUP BY C.ClassID, C.ClassName;
    ```

##### **5.9. Tìm các lớp có số lượng sinh viên lớn nhất.**
*   **Đại số Quan hệ:** (Phức tạp, cần nhiều bước gán và so sánh)
    1.  `ClassCounts ← ClassID 𝒢_{COUNT(StudentID) \text{ AS NumStudents}} (Student)`
    2.  `MaxNumStudents ← 𝒢_{MAX(NumStudents)} (ClassCounts)` (Lưu ý: Đây là một giá trị max, không phải quan hệ)
    3.  `σ_{NumStudents = MaxNumStudents} (ClassCounts)` (So sánh với giá trị max đã tìm được)
    4.  Kết quả join với `Class` để lấy thông tin lớp.
*   **SQL:**
    ```sql
    SELECT C.ClassID, C.ClassName, COUNT(S.StudentID) AS NumberOfStudents
    FROM Class C
    JOIN Student S ON C.ClassID = S.ClassID
    GROUP BY C.ClassID, C.ClassName
    HAVING COUNT(S.StudentID) = (
        SELECT MAX(StudentCount)
        FROM (
            SELECT COUNT(StudentID) AS StudentCount
            FROM Student
            GROUP BY ClassID
        ) AS SubQuery
    );
    ```
    Hoặc sử dụng CTE (Common Table Expressions):
    ```sql
    WITH ClassStudentCounts AS (
        SELECT ClassID, COUNT(StudentID) AS NumStudents
        FROM Student
        GROUP BY ClassID
    ), MaxStudents AS (
        SELECT MAX(NumStudents) AS MaxNum
        FROM ClassStudentCounts
    )
    SELECT C.ClassID, C.ClassName, CSC.NumStudents
    FROM Class C
    JOIN ClassStudentCounts CSC ON C.ClassID = CSC.ClassID
    JOIN MaxStudents MS ON CSC.NumStudents = MS.MaxNum;
    ```

##### **5.10. GPA (điểm trung bình) của sinh viên có mã (StudentID) = "T02".**
*(Giả sử GPA = Tổng điểm / Số môn đã học. Nếu có trọng số (tín chỉ) thì công thức sẽ khác)*
*   **Đại số Quan hệ:**
    `StudentID 𝒢_{AVG(Grades) \text{ AS GPA}} (σ_{StudentID='T02'} (StudentGrades))`
*   **SQL:**
    ```sql
    SELECT AVG(Grades) AS GPA
    FROM StudentGrades
    WHERE StudentID = 'T02';
    ```

##### **5.11. GPA cho mỗi sinh viên.**
*   **Đại số Quan hệ:**
    `StudentID 𝒢_{AVG(Grades) \text{ AS GPA}} (StudentGrades)`
    Kết quả join với `Student` để lấy tên sinh viên.
*   **SQL:**
    ```sql
    SELECT S.StudentID, S.StudentName, AVG(SG.Grades) AS GPA
    FROM Student S
    JOIN StudentGrades SG ON S.StudentID = SG.StudentID
    GROUP BY S.StudentID, S.StudentName;
    ```

##### **5.12. GPA của lớp có mã (ClassID) = "C02".**
*   **Đại số Quan hệ:**
    `π_{AVG(Grades)} ( (σ_{ClassID='C02'} (Student)) ⋈ StudentGrades )`
    Hoặc: `StudentID 𝒢_{AVG(Grades)} (StudentGrades)` sau đó lọc những sinh viên thuộc lớp C02 rồi tính trung bình của các GPA đó (cách này không đúng, vì là trung bình điểm của các sinh viên, không phải trung bình tất cả các điểm của sinh viên lớp đó).
    Cách đúng: Lấy tất cả điểm của sinh viên thuộc lớp C02 rồi tính trung bình.
    `Temp ← (σ_{ClassID='C02'} (Student)) ⋈ StudentGrades`
    `𝒢_{AVG(Grades) \text{ AS ClassGPA}} (Temp)` (gom nhóm không có thuộc tính nào)
*   **SQL:**
    ```sql
    SELECT AVG(SG.Grades) AS Class_C02_GPA
    FROM StudentGrades SG
    JOIN Student S ON SG.StudentID = S.StudentID
    WHERE S.ClassID = 'C02';
    ```

##### **5.13. GPA cho mỗi lớp.**
*   **Đại số Quan hệ:**
    `ClassID 𝒢_{AVG(Grades) \text{ AS ClassGPA}} (Student ⋈ StudentGrades)`
    Kết quả join với `Class` để lấy tên lớp.
*   **SQL:**
    ```sql
    SELECT C.ClassID, C.ClassName, AVG(SG.Grades) AS ClassGPA
    FROM Class C
    JOIN Student S ON C.ClassID = S.ClassID
    JOIN StudentGrades SG ON S.StudentID = SG.StudentID
    GROUP BY C.ClassID, C.ClassName;
    ```

##### **5.14. Tìm sinh viên có GPA cao nhất.**
*   **Đại số Quan hệ:** Tương tự câu 5.9, nhưng tính GPA trước.
    1.  `StudentGPAs ← StudentID 𝒢_{AVG(Grades) \text{ AS GPA}} (StudentGrades)`
    2.  `MaxGPAValue ← 𝒢_{MAX(GPA)} (StudentGPAs)`
    3.  `σ_{GPA = MaxGPAValue} (StudentGPAs)`
    4.  Kết quả join với `Student` để lấy thông tin sinh viên.
*   **SQL:**
    ```sql
    WITH StudentGPAs AS (
        SELECT StudentID, AVG(Grades) AS GPA
        FROM StudentGrades
        GROUP BY StudentID
    )
    SELECT S.StudentID, S.StudentName, SGA.GPA
    FROM Student S
    JOIN StudentGPAs SGA ON S.StudentID = SGA.StudentID
    WHERE SGA.GPA = (SELECT MAX(GPA) FROM StudentGPAs);
    ```
    Hoặc dùng `ORDER BY ... LIMIT 1` nếu chỉ cần 1 người và không quan tâm trường hợp bằng điểm.
    ```sql
    SELECT S.StudentID, S.StudentName, AVG(SG.Grades) AS GPA
    FROM Student S
    JOIN StudentGrades SG ON S.StudentID = SG.StudentID
    GROUP BY S.StudentID, S.StudentName
    ORDER BY GPA DESC
    LIMIT 1;
    ```

##### **5.15. Tìm sinh viên (ID và Tên) có GPA cao nhất.** (Tương tự 5.14)

##### **5.16. Tìm các lớp (ID và Tên) có GPA cao nhất.**
*   **SQL:**
    ```sql
    WITH ClassGPAs AS (
        SELECT C.ClassID, C.ClassName, AVG(SG.Grades) AS AvgGPA
        FROM Class C
        JOIN Student S ON C.ClassID = S.ClassID
        JOIN StudentGrades SG ON S.StudentID = SG.StudentID
        GROUP BY C.ClassID, C.ClassName
    )
    SELECT ClassID, ClassName, AvgGPA
    FROM ClassGPAs
    WHERE AvgGPA = (SELECT MAX(AvgGPA) FROM ClassGPAs);
    ```

##### **5.17. GPA có trọng số (tín chỉ) cho mỗi sinh viên.**
*(Công thức GPA có trọng số: `SUM(Grades * Units) / SUM(Units)`)*
*   **Đại số Quan hệ:** (Phức tạp hơn, cần tính toán trên các thuộc tính)
    1.  `GradesWithUnits ← StudentGrades ⋈ Subject`
    2.  `StudentWeightedScores ← StudentID 𝒢_{SUM(Grades * Units) \text{ AS SumWeightedScore}, SUM(Units) \text{ AS SumUnits}} (GradesWithUnits)`
    3.  `StudentWeightedGPA ← π_{StudentID, SumWeightedScore / SumUnits \text{ AS WeightedGPA}} (StudentWeightedScores)` (Phép chia này là một phép toán mở rộng)
*   **SQL:**
    ```sql
    SELECT
        S.StudentID,
        S.StudentName,
        SUM(SG.Grades * Sub.Units) * 1.0 / SUM(Sub.Units) AS WeightedGPA
        -- Nhân với 1.0 để đảm bảo phép chia là số thực
    FROM Student S
    JOIN StudentGrades SG ON S.StudentID = SG.StudentID
    JOIN Subject Sub ON SG.SubjectID = Sub.SubjectID
    GROUP BY S.StudentID, S.StudentName;
    ```

##### **5.18. GPA có trọng số cho mỗi sinh viên (ID và tên).** (Tương tự 5.17)

##### **5.19. GPA có trọng số cho mỗi lớp.**
*   **SQL:**
    ```sql
    SELECT
        C.ClassID,
        C.ClassName,
        SUM(SG.Grades * Sub.Units) * 1.0 / SUM(Sub.Units) AS ClassWeightedGPA
    FROM Class C
    JOIN Student S ON C.ClassID = S.ClassID
    JOIN StudentGrades SG ON S.StudentID = SG.StudentID
    JOIN Subject Sub ON SG.SubjectID = Sub.SubjectID
    GROUP BY C.ClassID, C.ClassName;
    ```

#### **6. Hiển thị tất cả các ràng buộc toàn vẹn (Show all integrity constraints).**

Việc này phụ thuộc vào DBMS:
*   **SQLite:**
    ```sql
    SELECT sql FROM sqlite_master WHERE type = 'table' AND name = 'TenBang';
    -- Lệnh trên sẽ hiển thị câu lệnh CREATE TABLE gốc, bao gồm các ràng buộc.
    -- Để xem trigger:
    SELECT sql FROM sqlite_master WHERE type = 'trigger';
    -- Để xem khóa ngoại (nếu đã bật):
    PRAGMA foreign_key_list('TenBang');
    PRAGMA index_list('TenBang'); -- Xem các index (PK, UNIQUE tạo index)
    PRAGMA index_info('TenIndex');
    ```
*   **MySQL:**
    ```sql
    SHOW CREATE TABLE TenBang;
    SHOW TRIGGERS FROM SMDB; -- Hoặc LIKE 'TenBang'
    SELECT * FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE TABLE_SCHEMA = 'SMDB' AND TABLE_NAME = 'TenBang';
    SELECT * FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE WHERE TABLE_SCHEMA = 'SMDB' AND TABLE_NAME = 'TenBang';
    ```
*   **PostgreSQL:**
    ```sql
    \d TenBang -- Trong psql
    SELECT conname, pg_get_constraintdef(oid)
    FROM pg_constraint
    WHERE conrelid = 'TenBang'::regclass;

    SELECT tgname, pg_get_triggerdef(oid)
    FROM pg_trigger
    WHERE tgrelid = 'TenBang'::regclass;
    ```
Bạn cần thay `TenBang` bằng tên các bảng (`Subject`, `Class`, `Student`, `StudentGrades`).

#### **7. Tkinter GUI cho cơ sở dữ liệu này (Tkinter GUI for this database).**

Phần này là một yêu cầu lập trình ứng dụng Python, không phải là truy vấn CSDL thuần túy. Nó đòi hỏi:
1.  Kết nối Python với CSDL (ví dụ dùng `sqlite3` module).
2.  Thiết kế giao diện người dùng bằng Tkinter (các cửa sổ, nhãn, ô nhập liệu, nút bấm, bảng hiển thị).
3.  Viết các hàm để:
    *   Hiển thị dữ liệu từ các bảng.
    *   Thêm, sửa, xóa dữ liệu cho các bảng (Subject, Class, Student, StudentGrades).
    *   Thực thi các truy vấn (ví dụ như các câu hỏi ở mục 5) và hiển thị kết quả.
    *   Có thể có các tính năng tìm kiếm, lọc.

Đây là một dự án nhỏ và cần nhiều thời gian để thực hiện. Nếu bạn cần ví dụ về một phần cụ thể (ví dụ: kết nối Python-SQLite, hiển thị dữ liệu lên Treeview của Tkinter), hãy cho biết.

---

Hy vọng phần giải chi tiết này sẽ giúp bạn hiểu rõ hơn về bài tập!