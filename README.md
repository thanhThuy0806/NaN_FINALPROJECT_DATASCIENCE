# Đồ án Cuối kỳ: Khoa học Dữ liệu (CSC17104)
## Đề tài: Phân tích và Khám phá Dữ liệu Game trên Nền tảng Steam

---

## 1. Thông tin Nhóm

| Họ và tên | MSSV | Vai trò |
|---|---|---|
| Phạm Xuân Duy | 24120295 | Thành viên |
| Hà Lê Thanh Thúy | 24120461 | Thành viên |
| Lê Thanh Phong | 24120409 | Thành viên |

> **Giảng viên hướng dẫn:** Giảng viên môn CSC17104 – Lập trình Khoa học Dữ liệu

---

## 2. Dataset

| Thông tin | Chi tiết |
|---|---|
| **Tên dataset** | Steam Games Dataset |
| **Nguồn** | <!-- URL Kaggle/nguồn gốc --> |
| **Tổ chức thu thập** | <!-- Tên tác giả / tổ chức --> |
| **Ngày thu thập** | <!-- dd/mm/yyyy --> |
| **License** | <!-- CC0 / CC BY / ... --> |
| **Số dòng (gốc)** | 29,931 records |
| **Số cột** | 18 cột |
| **Sau làm sạch** | 29,299 dòng |

**Các cột chính:** Appid, Name, Type, ReleaseDate, Genres, Developers, Publishers, Description, price, Tags, ReviewScore, PositiveReview, NegativeReview, OsRequirement, MemoryRequirement, CpuRequirement, Rank, Thumbnail

**Notebook/phân tích công khai liên quan:**
- <!-- Liệt kê các notebook Kaggle liên quan (nếu có) và giải thích câu hỏi của nhóm khác biệt như thế nào -->

---

## 3. Danh sách Câu hỏi Nghiên cứu

> Nhóm có **3 thành viên** → cần **6 câu hỏi** (2 câu/người), trong đó ít nhất 1 câu ML.

| # | Câu hỏi (tiêu đề ngắn) | Người phụ trách | Notebook | Tiêu chí |
|---|---|---|---|---|
| Q1 | <!-- Tiêu đề ngắn câu hỏi 1 --> | Xuân Duy | `notebooks/02_analysis_q1.ipynb` | <!-- D1–D6 --> |
| Q2 | <!-- Tiêu đề ngắn câu hỏi 2 --> | Xuân Duy | `notebooks/02_analysis_q2.ipynb` | <!-- D1–D6 --> |
| Q3 | <!-- Tiêu đề ngắn câu hỏi 3 --> | Thanh Thúy | `notebooks/02_analysis_q3.ipynb` | <!-- D1–D6 --> |
| Q4 | <!-- Tiêu đề ngắn câu hỏi 4 --> | Thanh Thúy | `notebooks/02_analysis_q4.ipynb` | <!-- D1–D6 --> |
| Q5 (ML) | <!-- Tiêu đề ngắn câu hỏi ML 1 --> | Thanh Phong | `notebooks/03_ml_q5.ipynb` | ML |
| Q6 (ML) | <!-- Tiêu đề ngắn câu hỏi ML 2 --> | Thanh Phong | `notebooks/03_ml_q6.ipynb` | ML |

---

## 4. Phân công công việc

| Thành viên | Nhiệm vụ |
|---|---|
| Xuân Duy | Thu thập & khám phá dữ liệu; Q1, Q2 |
| Thanh Thúy | Tiền xử lý dữ liệu; Q3, Q4 |
| Thanh Phong | Pipeline preprocessing (crawler, vectorDB, normalization); Q5, Q6 (ML) |

---

## 5. Kết quả Chính

> *Điền sau khi hoàn thành phân tích. Nêu 3–5 phát hiện quan trọng nhất, bao gồm phát hiện bất ngờ nhất.*

- <!-- Phát hiện 1 -->
- <!-- Phát hiện 2 -->
- <!-- Phát hiện 3 -->
- <!-- Phát hiện bất ngờ nhất -->

**Hạn chế:**
- <!-- Hạn chế về dữ liệu, phương pháp, và phạm vi nghiên cứu -->

---

## 6. Cài đặt Môi trường

Dự án sử dụng **Conda** để quản lý môi trường (Python 3.12).

### Bước 1 — Tạo môi trường (chạy 1 lần)

```bash
conda env create -f environment.yml
```

### Bước 2 — Kích hoạt và mở Jupyter

```bash
conda activate ds-steam-game
jupyter notebook
```

> **VS Code**: Mở notebook bất kỳ → **Select Kernel** → chọn `Python (ds-steam-game)`

---

## 7. Cài đặt Dịch vụ (ChromaDB + Ollama) — Tùy chọn

Chỉ cần thiết nếu muốn chạy lại pipeline preprocessing từ đầu.

```bash
# Khởi động ChromaDB và Ollama qua Docker
docker compose up -d

# Tải các model cần thiết
docker exec ollama ollama pull nomic-embed-text-v2-moe qwen3.5:2b
```

> **Lưu ý:** `chroma-data/` (vector database đã tính sẵn) được chia sẻ riêng qua Google Drive vì không được commit lên Git. Tải về và đặt vào thư mục gốc dự án trước khi chạy notebook vectorDB.

---

## 8. Hướng dẫn Chạy Notebook theo Thứ tự

```
1. notebooks/01_collection_exploration.ipynb   ← Khám phá dữ liệu gốc
2. notebooks/02_analysis_q1.ipynb              ← Phân tích Q1 (Xuân Duy)
3. notebooks/02_analysis_q2.ipynb              ← Phân tích Q2 (Xuân Duy)
4. notebooks/02_analysis_q3.ipynb              ← Phân tích Q3 (Thanh Thúy)
5. notebooks/02_analysis_q4.ipynb              ← Phân tích Q4 (Thanh Thúy)
6. notebooks/03_ml_q5.ipynb                   ← ML Q5 (Thanh Phong)
7. notebooks/03_ml_q6.ipynb                   ← ML Q6 (Thanh Phong)
```

**Dữ liệu đầu vào chung:** `data/processed/StreamGames_Cleaned_01.csv`
- SHA-256: `7DE4DF5D2C80097DAE14249F22C93F6DDFC192B9E3524D248227DAE1B222EE3E`
- Kiểm tra: `Get-FileHash .\data\processed\StreamGames_Cleaned_01.csv -Algorithm SHA256` (PowerShell)

> **Notebook preprocessing** (`notebooks/preprocessing_experiments/021–024`) là pipeline tạo ra file cleaned trên. Không bắt buộc chạy lại — bắt đầu từ file cleaned dùng chung là đủ.

---

## 9. Cấu trúc Repository

```
NaN_FINALPROJECT_DATASCIENCE/
├── README.md                          ← File này
├── environment.yml                    ← Conda environment
├── LLM_USAGE.md                       ← Log sử dụng LLM của từng thành viên
├── compose.yml                        ← Docker Compose (ChromaDB + Ollama)
├── data/
│   ├── raw/                           ← Dữ liệu gốc (không commit)
│   └── processed/                     ← Dữ liệu đã xử lý (không commit)
├── src/
│   └── preprocess/
│       ├── imputation/                ← Crawler + ChromaDB retrieval
│       └── normalized/                ← Chuẩn hóa CPU, OS, giá, ngày...
├── notebooks/
│   ├── 01_collection_exploration.ipynb
│   ├── 02_analysis_q1.ipynb ~ q4.ipynb
│   ├── 03_ml_q5.ipynb ~ q6.ipynb
│   └── preprocessing_experiments/
│       ├── 021_preprocess1_crawler.ipynb
│       ├── 022_preprocess1_vectordb.ipynb
│       ├── 023_preprocess1_norm_impu.ipynb
│       └── 024_preprocess1_deduplicate.ipynb
├── benchmark/
│   └── tags_retrieval.ipynb           ← Đánh giá hiệu năng ChromaDB retrieval
└── slides.pdf                         ← Slide trình bày (thêm trước khi nộp)
```
