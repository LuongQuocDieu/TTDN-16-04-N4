# 🚀 Quick Start - Predictive Lead Scoring

## ⚡ 5 Phút để Bắt Đầu

### 1️⃣ Xác Nhận Mô Hình Được Tải

```bash
# Kiểm tra xem model files tồn tại
ls -la custom-addons/model\ AI/lead_scoring_model*.pkl
```

✅ Tất cả 4 files nên có:
- `lead_scoring_model.pkl`
- `lead_scoring_model_scaler.pkl`
- `lead_scoring_model_encoders.pkl`
- `lead_scoring_model_features.pkl`

### 2️⃣ Mở Lead trong Odoo

1. Mở **CRM → Leads**
2. Chọn một Lead hoặc tạo Lead mới
3. Scroll xuống xem **AI Scoring Section**

### 3️⃣ Xem AI Score

Bạn sẽ thấy các trường:
- 📊 **Điểm dự đoán AI**: 45.78% (xác suất chuyển đổi)
- ✓ **Dự đoán chuyển đổi**: True/False
- 🎯 **Độ tin cậy**: 78.5%
- ⚠️ **Mức rủi ro**: Medium/High/Low

### 4️⃣ Cập Nhật Score (Tùy Chọn)

Nhấn **"Refresh AI Score"** để cập nhật ngay (thay vì đợi cron job)

### 5️⃣ Phân Tích Kết Quả

```
Điểm ≥ 80% → Rất cao: Follow-up nhanh! 🔥
Điểm 60-80% → Cao: Xử lý ngay 📢
Điểm 40-60% → Trung bình: Cần thêm info 📋
Điểm 20-40% → Thấp: Quyết định nhân viên 🤔
Điểm < 20% → Rất thấp: Cân nhắc loại bỏ ❌
```

## 📊 Dữ Liệu Model Sử Dụng

Model dự đoán dựa trên:

```
📌 Thông tin cơ bản:
   - Quy mô công ty
   - Ngân sách dự kiến

📌 Lịch sử tương tác:
   - Số cuộc gọi
   - Số email
   - Số cuộc họp

📌 Engagement:
   - Tỷ lệ phản hồi
   - Tỷ lệ mở email
   - Lượt xem trang

📌 Thời gian:
   - Tuổi lead
   - Thời gian từ tương tác cuối

📌 Đánh giá:
   - Điểm chất lượng thủ công
   - Mức ưu tiên
```

## 🔄 Tự Động Cập Nhật

**Cron job chạy hàng ngày** để cập nhật AI scores cho tất cả active leads.

Thời gian: Thường vào lúc **02:00 AM** (có thể cấu hình)

## 🎯 Trường Hợp Sử Dụng

### 1. Ưu Tiên Hóa Lead

```
SELECT leads
WHERE ai_will_convert = True
ORDER BY ai_score DESC
→ Tập trung vào Top 10 leads
```

### 2. Phân Công Công Việc

```
High risk leads (≥80%)
→ Giao cho senior sales
→ Follow-up trong 24h

Medium risk (40-60%)
→ Giao cho junior sales
→ Follow-up trong 3 ngày
```

### 3. Phân Tích Chiến Dịch

```
Phân tích leads từ source khác nhau
→ Cách nào tạo ra best leads?
→ Tối ưu hóa marketing spend
```

## 🧪 Test Mô Hình

### Tạo Lead Mẫu

```python
# Trong Odoo Python console
lead = env['crm.lead'].create({
    'name': 'Test Company',
    'company_size': '51-200',
    'budget': 500000,
    'quality_score': 80,
    'priority_btl': '3',  # High
})

print(f"AI Score: {lead.ai_score}%")
print(f"Will Convert: {lead.ai_will_convert}")
print(f"Risk Level: {lead.ai_risk_level}")
```

### Kiểm Tra Log

```bash
# Xem log AI scoring
tail -f odoo.log | grep "Lead scoring"
```

## 🔧 Troubleshooting

### ❌ AI Score không hiển thị?

```
→ Kiểm tra: Model files có tồn tại không?
→ Kiểm tra: Lead có đủ dữ liệu không?
→ Kiểm tra: Log files có error không?
```

### ❌ Lỗi Import?

```python
# Trong Odoo terminal:
python -c "from model_AI import get_lead_scoring_service; print('OK')"

# Nếu lỗi → cài dependencies:
pip install scikit-learn pandas numpy
```

### ❌ Model trả về default score?

```
→ Có thể model files corrupt
→ Copy lại các .pkl files từ training
```

## 📈 Cải Thiện Model

Để cải thiện độ chính xác:

```python
from model_AI.predictive_lead_scoring_trainer import PredictiveLeadScoringTrainer
import pandas as pd

# 1. Export dữ liệu thực từ Odoo
df = pd.read_csv('leads_data.csv')

# 2. Huấn luyện lại
trainer = PredictiveLeadScoringTrainer()
results = trainer.train(df)

# 3. Lưu model mới
trainer.save_model('lead_scoring_model')

# 4. Restart Odoo
```

## 📞 Liên Hệ

Có câu hỏi? Xem các file:
- `PREDICTIVE_LEAD_SCORING_GUIDE.md` - Hướng dẫn chi tiết
- `IMPLEMENTATION_SUMMARY.md` - Tóm tắt kỹ thuật
- Hoặc xem comment trong code

---

**Chúc bạn thành công! 🎉**

Bây giờ AI của bạn sẽ:
✅ Tự động dự đoán chất lượng lead
✅ Giúp nhân viên ưu tiên hóa công việc
✅ Tăng tỷ lệ chuyển đổi
✅ Tiết kiệm thời gian
