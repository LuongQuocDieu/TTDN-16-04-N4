# Hướng Dẫn Sử Dụng AI Predictive Lead Scoring
# Guide to Using AI Predictive Lead Scoring

## 🚀 Bắt Đầu Nhanh / Quick Start

### Bước 1: Truy cập Odoo
- URL: http://localhost:8069/web
- Username: admin
- Password: admin

### Bước 2: Mở CRM - Khách hàng tiềm năng
1. Menu → CRM → Khách hàng tiềm năng
2. Hoặc: http://localhost:8069/web#action=crm.crm_lead_action_pipeline

### Bước 3: Xem AI Score
1. Chọn một Lead từ danh sách
2. Kéo xuống tìm tab "🤖 AI Predictive Scoring" (thứ 3 từ trên)
3. Xem các thông số:
   - **Điểm dự đoán AI (%)**: 0-100%
   - **Dự đoán chuyển đổi**: Có/Không
   - **Độ tin cậy (%)**: 0-100%
   - **Mức rủi ro**: Rất cao, Cao, Trung bình, Thấp, Rất thấp

---

## 📊 Diễn Giải Kết Quả / Interpreting Results

### AI Score Ranges

**🔴 Rất Cao (80-100%)**
- Lead này rất có khả năng chuyển đổi
- **Hành động**: Follow-up NGAY, ưu tiên cao
- **Ví dụ**: Công ty ABC Technology (85%), Tập đoàn XYZ Retail (90%)

**🟠 Cao (60-80%)**
- Lead này có tiềm năng cao
- **Hành động**: Follow-up trong vài ngày, chuẩn bị báo giá
- **Ví dụ**: Công ty DEF Manufacturing (75%), Công ty GHI Real Estate (80%)

**🟡 Trung bình (40-60%)**
- Lead này có tiềm năng vừa phải
- **Hành động**: Tiếp tục nuôi dưỡng (nurture), thu thập thêm thông tin
- **Ví dụ**: Phòng khám MNO Health (55%), Tập đoàn VWX Logistics (65%)

**🟢 Thấp (20-40%)**
- Lead này có khả năng chuyển đổi thấp
- **Hành động**: Để dành hoặc loại bỏ, tập trung vào leads khác
- **Ví dụ**: Startup YZA Innovations (30%), Công ty BCD Import (35%)

**⚪ Rất Thấp (<20%)**
- Lead này không phù hợp
- **Hành động**: Loại bỏ khỏi danh sách chính
- **Ví dụ**: Quán Cà phê ABC Coffee (20%), Dự án EFG Properties (40%)

---

## 🎯 Mức Rủi Ro / Risk Levels

| Mức Rủi Ro | AI Score | Ý Nghĩa | Hành Động |
|-----------|----------|--------|----------|
| 🔴 Rất cao | ≥80% | Rất có khả năng chuyển đổi nhưng cần confirm | Follow-up ngay |
| 🟠 Cao | 60-80% | Có khả năng cao | Ưu tiên, chuẩn bị báo giá |
| 🟡 Trung bình | 40-60% | Tùy thuộc vào yếu tố khác | Nuôi dưỡng, tìm hiểu nhu cầu |
| 🟢 Thấp | 20-40% | Ít khả năng | Để dành hoặc loại bỏ |
| ⚪ Rất thấp | <20% | Không phù hợp | Loại bỏ |

---

## 📈 Các Yếu Tố Ảnh Hưởng / Affecting Factors

Mô hình AI xem xét:

### 1️⃣ **Quy Mô Công Ty** (Company Size)
- Công ty lớn (200+) → Điểm cao hơn
- Startup/nhỏ (<10) → Điểm thấp hơn

### 2️⃣ **Ngân Sách** (Budget)
- Budget cao (>500K) → Điểm cao hơn
- Budget thấp (<50K) → Điểm thấp hơn

### 3️⃣ **Tương Tác** (Interactions)
- Nhiều cuộc gọi/email/họp → Điểm cao hơn
- Không có tương tác → Điểm thấp hơn

### 4️⃣ **Tần Suất Tương Tác** (Recency)
- Tương tác gần đây → Điểm cao hơn
- Không tương tác lâu → Điểm thấp hơn

### 5️⃣ **Chất Lượng Lead** (Quality Score)
- Score cao (80+) → Điểm dự đoán cao hơn
- Score thấp (<30) → Điểm dự đoán thấp hơn

### 6️⃣ **Độ Tuổi Lead** (Lead Age)
- Lead mới → Có chuyển đổi cao hơn
- Lead cũ (>90 ngày) → Độ tin cậy giảm

---

## 💾 Làm Mới AI Score / Refresh AI Score

### Cách 1: Tự động
- Hệ thống tự động cập nhật AI Score khi:
  - Mở form Lead
  - Cập nhật thông tin Lead
  - Cron job chạy hàng ngày lúc 2:00 AM

### Cách 2: Thủ công
1. Mở Lead form
2. Tìm nút "Cập nhật AI Score" trên header
3. Nhấp để làm mới ngay lập tức

---

## 📋 Dữ Liệu Mẫu / Demo Data Included

Đã tạo 14 mẫu Lead để kiểm tra:

| Tên Công Ty | Ngành | Quy Mô | Ngân Sách | AI Score |
|------------|-------|-------|----------|----------|
| ABC Technology | Công nghệ | 51-200 | 500K | ~85% |
| XYZ Retail | Bán lẻ | 201-500 | 1M | ~90% |
| DEF Manufacturing | Sản xuất | 11-50 | 250K | ~75% |
| GHI Real Estate | Bất động sản | 51-200 | 750K | ~80% |
| JKL Finance | Tài chính | 201-500 | 1M | ~88% |
| MNO Health | Y tế | 11-50 | 100K | ~55% |
| PQR Education | Giáo dục | 51-200 | 200K | ~60% |
| STU Services | Dịch vụ | 1-10 | 50K | ~25% |
| VWX Logistics | Dịch vụ | 201-500 | 400K | ~65% |
| YZA Innovations | Công nghệ | 1-10 | 25K | ~30% |
| ABC Coffee | Bán lẻ | 1-10 | 10K | ~20% |
| BCD Import | Bán lẻ | 11-50 | 30K | ~35% |
| EFG Properties | Bất động sản | 51-200 | 100K | ~40% |
| HIJ Consulting | Dịch vụ | 11-50 | 75K | ~45% |

---

## 🔧 Cấu Hình / Configuration

### Tệp Mô Hình / Model Files
```
custom-addons/model AI/
├── lead_scoring_model.pkl           # Gradient Boosting Model
├── lead_scoring_model_scaler.pkl    # Feature Scaler
├── lead_scoring_model_encoders.pkl  # Category Encoders
└── lead_scoring_model_features.pkl  # Feature Registry
```

### Dịch Vụ / Service
```
custom-addons/model AI/lead_scoring_service.py
- Singleton pattern cho prediction
- Auto-loads model trên first access
- Thread-safe implementation
```

### Fields Được Tạo / Fields Created
```sql
ALTER TABLE crm_lead ADD COLUMN
  ai_score FLOAT8,                  -- Điểm dự đoán (0-100)
  ai_will_convert BOOLEAN,          -- Dự đoán chuyển đổi
  ai_confidence FLOAT8,             -- Độ tin cậy (0-100)
  ai_risk_level VARCHAR,            -- Mức rủi ro
  ai_last_update TIMESTAMP;         -- Cập nhật lần cuối
```

---

## ✅ Kiểm Tra Hoạt Động / Verification Checklist

- [ ] Odoo đang chạy (http://localhost:8069)
- [ ] Có thể đăng nhập với admin/admin
- [ ] Có thể mở CRM → Khách hàng tiềm năng
- [ ] Có thể xem tab "🤖 AI Predictive Scoring" trong Lead form
- [ ] AI Score hiển thị giá trị (không phải lỗi)
- [ ] Mức rủi ro hiển thị chính xác
- [ ] Ngày cập nhật cuối được ghi lại

---

## 🚨 Khắc Phục Sự Cố / Troubleshooting

### ❌ Tab "AI Predictive Scoring" không hiển thị
**Giải pháp**: Refresh trang Odoo (F5 hoặc Ctrl+R)

### ❌ AI Score hiển thị 0 hoặc error
**Giải pháp**: 
- Kiểm tra model files có tồn tại không
- Restart Odoo container: `docker restart odoo_app_fitdnu`
- Kiểm tra logs: `docker logs odoo_app_fitdnu`

### ❌ Demo leads không hiển thị
**Giải pháp**: 
- Refresh Odoo page
- Kiểm tra database: `psql -U manh -d manh -c "SELECT COUNT(*) FROM crm_lead;"`

### ❌ Model không load
**Giải pháp**:
- Kiểm tra Python files trong model AI folder
- Kiểm tra permissions: `docker exec odoo_app_fitdnu ls -la /mnt/custom-addons/model\ AI/`

---

## 📞 Hỗ Trợ / Support

Để kiểm tra trạng thái hệ thống:
```bash
# Xem logs Odoo
docker logs odoo_app_fitdnu

# Kiểm tra database
docker exec postgres_odoo_fitdnu psql -U manh -d manh -c "SELECT COUNT(*) FROM crm_lead;"

# Kiểm tra mô hình
docker exec postgres_odoo_fitdnu psql -U manh -d manh -c "SELECT COUNT(*) FROM ir_model_fields WHERE model='crm.lead';"
```

---

## 📝 Ghi Chú / Notes

- **Độ chính xác mô hình**: ~64% trên test data
- **Kiểu mô hình**: Gradient Boosting Classifier
- **Số features**: 12 features đã được chọn
- **Training samples**: 500 mẫu
- **Update frequency**: Tự động 2AM hàng ngày + thủ công theo nhu cầu

---

**Tạo ngày**: 2026-01-23
**Phiên bản**: 1.0
**Status**: ✅ Hoạt động bình thường
