Bạn là một Giảng viên Java giàu kinh nghiệm, có khả năng giảng dạy trực quan và giúp sinh viên dễ ghi nhớ các khái niệm phức tạp.

Hãy đọc đoạn tài liệu về Java Garbage Collection (GC) dưới đây và thực hiện các yêu cầu:

1. Tóm tắt nội dung dưới dạng bảng so sánh giữa Young Generation và Old Generation.

2. Bảng phải có các cột:

    * Tiêu chí
    * Young Generation
    * Old Generation

3. Bảng phải so sánh theo các tiêu chí:

    * Các vùng con bên trong
    * Loại đối tượng lưu trữ
    * Điều kiện kích hoạt GC
    * Loại GC tương ứng
    * Tốc độ thực thi của GC

4. Sau bảng, hãy tạo một sơ đồ ASCII đơn giản mô tả đường đi của một đối tượng từ lúc được tạo bằng từ khóa new cho đến khi được thăng cấp (Promoted) sang Old Generation.

5. Giải thích ngắn gọn (2–3 dòng) ý nghĩa của sơ đồ.

6. Chỉ sử dụng thông tin xuất hiện trong tài liệu được cung cấp, không bổ sung kiến thức ngoài tài liệu.

Tài liệu:

[Đính kèm đoạn văn về Java Garbage Collection]



# Tóm tắt Java Garbage Collection (GC)

| Tiêu chí | Young Generation | Old Generation |
|-----------|------------------|----------------|
| Các vùng con bên trong | Eden Space, Survivor S0, Survivor S1 | Không được chia nhỏ trong tài liệu |
| Loại đối tượng lưu trữ | Đối tượng mới được tạo và các đối tượng còn sống sau Minor GC | Đối tượng có thời gian sống dài, đã tồn tại qua nhiều lần Minor GC |
| Điều kiện kích hoạt GC | Eden Space đầy | Old Generation đầy |
| Loại GC tương ứng | Minor GC | Major GC / Full GC |
| Tốc độ thực thi của GC | Nhanh hơn | Chậm hơn đáng kể |
| Ảnh hưởng đến hệ thống | Tác động ít hơn | Có thể Stop-the-world, dừng toàn bộ ứng dụng |

---

# Sơ đồ đường đi của đối tượng

        new
         |
         v
    +-----------+
    |   Eden    |
    +-----------+
         |
         | Eden đầy
         v
     Minor GC
         |
         v
    +-----------+
    | Survivor  |
    |  S0 / S1  |
    +-----------+
         |
         | Sống sót nhiều lần
         | qua Minor GC
         v
    +-----------+
    | Old Gen   |
    +-----------+
         |
         | Old Gen đầy
         v
      Full GC
(Major GC)

Giải thích:
- Đối tượng mới được tạo sẽ nằm trong Eden Space.
- Sau khi sống sót qua các đợt Minor GC, đối tượng được chuyển sang Survivor.
- Khi đạt ngưỡng tuổi nhất định, đối tượng được thăng cấp (Promoted) sang Old Generation.
- Khi Old Generation đầy, Major GC hoặc Full GC sẽ được kích hoạt để dọn dẹp bộ nhớ.