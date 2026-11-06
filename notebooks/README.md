# Đồ án Khoa học Dữ liệu: Steam Games

## Cấu trúc repository

```text
data/
  raw/          Dữ liệu gốc đã tải/thu thập (hiện chưa có trong repository)
  processed/    Dữ liệu đã làm sạch và các phiên bản xử lý tiếp theo
src/            Các module Python có thể tái sử dụng
notebooks/
  00_questioning.ipynb
  01_collection_exploration.ipynb
  02_analysis_q1.ipynb
  02_analysis_q2.ipynb
  02_analysis_q3.ipynb
  02_analysis_q4.ipynb
  03_ml_q5.ipynb
  03_ml_q6.ipynb
  preprocessing_experiments/
    021_preprocess1_crawler.ipynb
    022_preprocess1_vectordb.ipynb
    023_preprocess1_norm_impu.ipynb
```

`data/processed/StreamGames_Cleaned_01.csv` là dữ liệu đã làm sạch cơ bản, được
dùng làm đầu vào chung cho cả nhóm (29.299 dòng, 19 cột). Giữ nguyên file này;
nếu cần xử lý thêm, hãy lưu thành file phiên bản mới thay vì ghi đè.

Dữ liệu gốc hiện chưa được lưu trong `data/raw/`. Nhóm cần ghi rõ nguồn, URL,
ngày thu thập và giấy phép sử dụng; chỉ thêm dữ liệu gốc vào repository nếu
được phép và cần thiết để tái lập quy trình.

## Chuẩn bị dữ liệu

File dữ liệu không được push lên Git vì các thành viên đã có bản sao. Mỗi người
đặt file của mình tại:

```bash
data/processed/StreamGames_Cleaned_01.csv
```

Không đổi tên file và không ghi đè lên dữ liệu gốc này. Để chắc chắn các thành
viên đang dùng cùng một phiên bản, kiểm tra mã SHA-256:

- **Nếu dùng PowerShell:**
  ```powershell
  Get-FileHash .\data\processed\StreamGames_Cleaned_01.csv -Algorithm SHA256
  ```
- **Nếu dùng Command Prompt (CMD):**
  ```cmd
  certutil -hashfile .\data\processed\StreamGames_Cleaned_01.csv SHA256
  ```
- **Nếu dùng Ubuntu / WSL / Linux:**
  ```bash
  sha256sum data/processed/StreamGames_Cleaned_01.csv
  ```

Giá trị chuẩn của bản hiện tại:
`7DE4DF5D2C80097DAE14249F22C93F6DDFC192B9E3524D248227DAE1B222EE3E`  
Nếu kết quả khác, hãy trao đổi và thống nhất file chuẩn trước khi phân tích.
Thư mục `data/processed/` đã được Git bỏ qua nên file cục bộ sẽ không bị commit.

## Cài đặt môi trường

Dự án sử dụng Conda để quản lý môi trường. Các thành viên có thể sử dụng **Miniconda** (khuyên dùng vì rất nhẹ ~90MB) hoặc **Anaconda**.

### 1. Kiểm tra máy đã có Miniconda / Conda chưa

Mở **PowerShell** và chạy một trong hai lệnh sau:

- **Cách 1: Kiểm tra lệnh `conda` có sẵn không:**
  ```powershell
  conda --version
  ```

- **Cách 2: Kiểm tra đường dẫn cài đặt của Miniconda:**
  ```powershell
  Test-Path "$env:USERPROFILE\miniconda3\Scripts\conda.exe"
  ```
  *(Nếu trả về `True` là máy đã có Miniconda)*

### 2. Tải và cài đặt nhanh (nếu máy chưa có)

- **Cách 1 (Tải trực tiếp):** Tải file cài đặt [Miniconda Windows (64-bit)](https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe) và bấm Next cài đặt mặc định (khoảng 1 phút).
- **Cách 2 (Cài bằng 1 dòng lệnh Windows):** Mở PowerShell/CMD gõ:
  ```powershell
  winget install Anaconda.Miniconda3
  ```

### 3. Kích hoạt và cấu hình Conda cho PowerShell (Chạy 1 lần duy nhất)

Sau khi cài xong, nếu mở PowerShell thông thường mà gõ `conda` báo lỗi chưa nhận diện, bạn chỉ cần chạy 2 dòng sau:

```powershell
# Kích hoạt ngay trong cửa sổ PowerShell hiện tại:
& "$env:USERPROFILE\miniconda3\Scripts\conda.exe" "shell.powershell" "hook" | Out-String | Invoke-Expression

# Đăng ký vĩnh viễn cho PowerShell:
conda init powershell
```

*(Chạy xong, tắt cửa sổ PowerShell đi mở lại là từ đó về sau gõ `conda` ở đâu cũng được)*

### 4. Tạo môi trường và khởi động Notebook

**Bước tạo môi trường ban đầu (Chỉ chạy 1 lần duy nhất khi mới clone dự án):**
```bash
# Đứng tại thư mục gốc của dự án và chạy:
conda env create -f environment.yml
```

**Quy trình mở máy làm việc hàng ngày:**
```bash
# 1. Kích hoạt môi trường của dự án
conda activate ds-steam-game

# 2. Khởi động Jupyter Notebook
jupyter notebook
```

*(Lưu ý nếu code trong **VS Code**: mở bất kỳ notebook nào trong thư mục `notebooks/`, bấm **Select Kernel** ở góc trên bên phải $\rightarrow$ chọn môi trường **`Python (ds-steam-game)`**)*

## Thứ tự làm việc với notebook

1. `01_collection_exploration.ipynb`: ghi nguồn và giấy phép dữ liệu, khảo sát
   chất lượng dữ liệu, tổng kết 3–5 nhận xét chính.
2. Với bốn câu hỏi non-ML, mỗi owner làm trong một notebook riêng:
   `02_analysis_q1.ipynb` đến `02_analysis_q4.ipynb`. Bắt đầu từ
   `StreamGames_Cleaned_01.csv`; giải thích các bước xử lý và thay đổi số dòng,
   nêu lý do chọn phương pháp, đưa ra câu trả lời trực tiếp với kết quả cụ thể
   và ít nhất hai biểu đồ có nhãn rõ ràng.
3. Với hai câu hỏi ML, mỗi owner làm một notebook riêng:
   `03_ml_q5.ipynb` và `03_ml_q6.ipynb`. Mỗi notebook cần so sánh baseline đơn
   giản với ít nhất hai mô hình, chọn cách chia tập phù hợp, tránh rò rỉ dữ liệu,
   chỉ tinh chỉnh trên tập train, đánh giá trên tập test một lần, phân tích lỗi
   và giải thích mô hình.
4. Khi hoàn tất, thêm bài trình bày cuối cùng với tên `slides.pdf`.

Các notebook `021`–`023` là thử nghiệm/hỗ trợ tiền xử lý, không thay thế notebook
trả lời câu hỏi nghiên cứu. Notebook crawler có thể chạy nhiều giờ và cần dữ liệu
gốc. Notebook vector database cần dịch vụ/dữ liệu ChromaDB và dữ liệu kiểm thử.
Các notebook này không bắt buộc với thành viên bắt đầu từ file cleaned dùng chung.
Notebook `023_preprocess1_norm_impu.ipynb` đọc file cleaned dùng chung và ghi ra
một phiên bản đã xử lý tiếp theo.

## Quy ước làm việc nhóm

- Mỗi thành viên phụ trách hai câu hỏi. Nhóm có `n` thành viên cần có `2 × n`
  câu hỏi; mỗi câu hỏi có một người phụ trách chính. Bốn câu non-ML và hai câu
  ML tương ứng với yêu cầu này nếu nhóm có ba thành viên. Đề chỉ yêu cầu ít nhất
  một câu ML; hai câu ML vẫn được, miễn mỗi câu có câu hỏi dự đoán rõ ràng.
- Câu hỏi, động cơ, phương pháp và kết quả chi tiết được ghi trong notebook riêng
  tương ứng; không cần chép lại nội dung dài ở một notebook tổng hợp. Mỗi câu
  non-ML cần dùng ít nhất hai tiêu chí D1–D6; tổng thể các câu non-ML cần bao
  quát ít nhất bốn tiêu chí.
- Mỗi câu hỏi dùng một notebook riêng và một nhánh riêng, ví dụ
  `analysis/q1-price` hoặc `ml/q5-rating`. Không để nhiều người cùng sửa một
  notebook. Tạo nhánh từ phiên bản mới nhất của nhánh chính; sau đó tạo pull
  request chỉ gồm notebook của câu hỏi đó và các thay đổi liên quan trực tiếp.
- Để tránh conflict, chỉ một người điều phối cập nhật bảng mục lục câu hỏi trong
  README sau khi nhóm chốt câu hỏi. Những người khác ghi kết quả trong notebook
  riêng rồi gửi pull request; không chỉnh sửa đồng thời các file dùng chung.
- Notebook không nên chứa output lớn: trước khi commit, chọn **Clear All Outputs**
  trong Jupyter. Đừng commit dữ liệu sinh ra, file cleaned mới, ChromaDB/Ollama
  hoặc checkpoint.
- Xem file cleaned dùng chung là chỉ đọc. Không commit file sinh ra kích thước
  lớn, dữ liệu ChromaDB/Ollama hoặc notebook checkpoint.
- Ghi lại các lần sử dụng LLM đáng kể trong `LLM_USAGE.md`.

README chỉ cần làm bảng mục lục ngắn với tên/câu hỏi, người phụ trách và notebook;
không cần chép lại động cơ, phương pháp hay nội dung phân tích đã có trong
notebook tương ứng.

| Câu hỏi (ghi tiêu đề ngắn) | Người phụ trách | Notebook | Tiêu chí (D1–D6) |
|---|---|---|---|
| Q1 | Xuân Duy | `02_analysis_q1.ipynb` | Điền |
| Q2 | Xuân Duy | `02_analysis_q2.ipynb` | Điền |
| Q3 | Thanh Thúy | `02_analysis_q3.ipynb` | Điền |
| Q4 | Thanh Thúy | `02_analysis_q4.ipynb` | Điền |
| Q5 (ML) | Thanh Phong | `03_ml_q5.ipynb` | ML |
| Q6 (ML) | Thanh Phong | `03_ml_q6.ipynb` | ML |

Thay Q1–Q6 bằng tiêu đề ngắn của câu hỏi tương ứng. Trước khi nộp, cập nhật
README với họ tên/MSSV, bảng phân công, nguồn và giấy phép dữ liệu, phát hiện
chính và hạn chế của nghiên cứu.
