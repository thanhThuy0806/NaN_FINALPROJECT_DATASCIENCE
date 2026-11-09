# Đồ án Cuối kỳ: Khoa học Dữ liệu (CSC17104)
## Đề tài: Phân tích và Khám phá Dữ liệu Game trên Nền tảng Steam

---

### 1. Thông tin Nhóm và Giảng viên
- **Giảng viên hướng dẫn:** Thầy/Cô phụ trách môn Khoa học Dữ liệu
- **Nhóm sinh viên thực hiện:**

| STT | Họ và tên | MSSV | Vai trò / Câu hỏi phụ trách |
|:---:|:---|:---:|:---|
| 1 | Phạm Xuân Duy | 24120295 | Câu hỏi Q1, Q2 |
| 2 | Hà Lê Thanh Thúy | 24120... | Câu hỏi Q3, Q4 |
| 3 | Lê Thanh Phong | 24120... | Câu hỏi Q5 (ML), Q6 (ML) |

---

### 2. Giới thiệu đề tài & Dữ liệu
- **Mục tiêu:** Phân tích các yếu tố ảnh hưởng đến độ phổ biến, doanh thu, đánh giá của người chơi và cấu hình phần cứng của các tựa game trên nền tảng Steam; xây dựng các mô hình Machine Learning dự đoán và phân loại.
- **Tập dữ liệu:** Dữ liệu được trích xuất từ Steam Store và Steam Web API, phục vụ mục đích giáo dục và nghiên cứu học thuật. Nhóm tự xây dựng pipeline phân tích độc lập, không sao chép các notebook có sẵn trên Kaggle.
- **Dữ liệu đã làm sạch:** `data/processed/StreamGames_Cleaned_01.csv` là dữ liệu đã làm sạch cơ bản, được dùng làm đầu vào chung cho cả nhóm (29.299 dòng, 19 cột). Giữ nguyên file này; nếu cần xử lý thêm, hãy lưu thành file phiên bản mới thay vì ghi đè.
- **Dữ liệu gốc:** Dữ liệu gốc hiện chưa được lưu trong `data/raw/`. Nhóm cần ghi rõ nguồn, URL, ngày thu thập và giấy phép sử dụng; chỉ thêm dữ liệu gốc vào repository nếu được phép và cần thiết để tái lập quy trình.

---

### 3. Cấu trúc Repository

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
environment.yml
LLM_USAGE.md
README.md
slides.pdf
```

```bash
# Run docker and detach
docker compose up -d

# Pull requirement models
docker exec ollama ollama pull nomic-embed-text-v2-moe qwen3.5:2b
```

## Preprocess
The guide below show you how to run the preprocess pipeline so you can recreate **data cleaned version** from **provided data**
### Crawler

### VectorDB retrieval

### Normalization and Imputation

*Note*: It is **not recommneded** to run this in the pipeline entirely because the total it consumes is **about 6-10 hours of waiting**. Instead, you should use and cleaned version after 2 first processes in **021_preprocess1_crawler.ipynb** and **022_preprocess1_vectordb.ipynb**. The **chroma-data**( because the **vector database the project used is chromadb**), will be provided separately so you can download it and **try retrieval process**

- Craw for missing value: Run **021_preprocess1_crawler.ipynb** with fallback using LLM model to fill out missing value that failed to crawl  

- Vector database embbed and retrieval: Run **022_preprocess2_vectordb.ipynb**

- Normalize and Impute can be found in **023_preprocess1_norm_impu.ipynb**
