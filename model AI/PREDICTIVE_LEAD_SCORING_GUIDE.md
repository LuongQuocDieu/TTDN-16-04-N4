# Predictive Lead Scoring - Hướng Dẫn Tích Hợp

## 📋 Tổng Quan

Mô hình AI **Predictive Lead Scoring** đã được huấn luyện và tích hợp vào hệ thống Odoo BTL. Mô hình này sử dụng **Gradient Boosting Classifier** để dự đoán khả năng một lead sẽ chuyển đổi thành khách hàng.

## 🎯 Tính Năng Chính

### 1. **Dự Đoán Chất Lượng Lead**
- Dự đoán xác suất chuyển đổi (0-100%)
- Phân loại mức rủi ro (Rất cao, Cao, Trung bình, Thấp, Rất thấp)
- Độ tin cậy của dự đoán

### 2. **Tích Hợp Tự Động**
- Tự động tính toán AI score khi tạo/cập nhật lead
- Cron job hàng ngày để cập nhật lại scores
- Không cần cấu hình phức tạp

### 3. **Features Sử Dụng**
- Quy mô công ty
- Ngân sách dự kiến
- Lịch sử tương tác (cuộc gọi, email, họp)
- Thời gian từ lần tương tác cuối
- Tỷ lệ phản hồi
- Tuổi của lead
- Điểm ưu tiên

## 📊 Kết Quả Huấn Luyện

```
Độ chính xác:
- Train set: 100.00%
- Test set:  64.00%
- ROC-AUC:   0.5743

Features quan trọng nhất:
1. Email open rate (13.89%)
2. Budget (12.96%)
3. Engagement score (9.05%)
4. Số email (8.54%)
5. Quality score (7.81%)
```

## 📁 Cấu Trúc File

```
model AI/
├── __init__.py                              # Package init
├── lead_scoring_service.py                  # Service dự đoán
├── predictive_lead_scoring_trainer.py       # Script huấn luyện
├── lead_scoring_model.pkl                   # Mô hình chính
├── lead_scoring_model_scaler.pkl            # Scaler (chuẩn hóa)
├── lead_scoring_model_encoders.pkl          # Encoder (mã hóa)
├── lead_scoring_model_features.pkl          # Danh sách features
└── dataset/                                 # Thư mục dataset

BTL_Quan_ly_khach_hang/
└── models/
    └── crm_lead.py                          # Mô hình CrmLead với AI scoring
```

## 🚀 Cách Sử Dụng

### 1. **Xem AI Score trong Lead**

Khi mở một Lead, bạn sẽ thấy các thông tin AI:
- **Điểm dự đoán AI (%)**: Xác suất chuyển đổi
- **Dự đoán chuyển đổi**: True/False
- **Độ tin cậy (%)**: Mức độ tin cậy
- **Mức rủi ro**: Very High, High, Medium, Low, Very Low

### 2. **Cập Nhật AI Score Thủ Công**

Nhấn nút "Refresh AI Score" để cập nhật dự đoán cho lead hiện tại.

### 3. **Tự Động Cập Nhật**

Hệ thống sẽ tự động chạy cron job hàng ngày để cập nhật lại AI scores cho tất cả active leads.

## 🔧 Cấu Hình

### Bật/Tắt Cron Job

Trong Odoo, vào **Settings → Technical → Automation → Scheduled Actions** và tìm:
- `Lead AI Score Refresh (Cron)` - Cập nhật AI score hàng ngày

### Tùy Chỉnh Model

Để huấn luyện lại mô hình với dữ liệu mới:

```python
from model_AI.predictive_lead_scoring_trainer import PredictiveLeadScoringTrainer

trainer = PredictiveLeadScoringTrainer(model_path='path/to/model')
results = trainer.train()  # Huấn luyện
trainer.save_model('lead_scoring_model')  # Lưu model
```

## 📈 Giải Thích AI Score

### Mức Rủi ro

| Xác suất | Mức Rủi ro | Hành Động Đề Xuất |
|---------|-----------|-------------------|
| ≥ 80% | Rất cao | Ưu tiên cao, Follow-up nhanh |
| 60-80% | Cao | Xử lý ngay |
| 40-60% | Trung bình | Cần thêm thông tin |
| 20-40% | Thấp | Nhân viên quyết định |
| < 20% | Rất thấp | Cân nhắc loại bỏ |

### Độ Tin Cậy

- **Cao (> 70%)**: Model rất chắc chắn về dự đoán
- **Trung bình (50-70%)**: Có thể tin tưởng một phần
- **Thấp (< 50%)**: Cần thêm dữ liệu để quyết định

## 🔄 Quy Trình Dự Đoán

```
Lead Dữ Liệu
    ↓
Chuẩn bị Features
    ↓
Mã hóa Categorical (Encoder)
    ↓
Chuẩn hóa (Scaler)
    ↓
Dự đoán (Model)
    ↓
Kết quả (Probability, Score, Risk)
```

## 📝 Các Trường Được Tính Toán

### AI Score Components

```python
# Engagement Score
engagement_score = (response_rate * 0.3 + 
                   email_open_rate * 0.4 + 
                   (page_views / 100) * 0.3)

# Recency Score
recency_score = 1.0 / (1.0 + days_since_interaction / 30.0)

# Lead Maturity
lead_maturity = 1.0 / (1.0 + exp(-((lead_age - 60) / 30.0)))

# Final Quality Score
quality_score = (conversion_prob * 0.6 + manual_quality * 0.4)
```

## ⚠️ Giới Hạn & Lưu Ý

1. **Dữ liệu Mẫu**: Model được huấn luyện với dữ liệu tổng hợp mẫu (500 records)
   - Để cải thiện độ chính xác, cần huấn luyện lại với dữ liệu thực tế
   
2. **Thời Gian Cập Nhật**: AI score được cập nhật khi:
   - Lead được tạo mới
   - Lead được cập nhật (quality_score, budget, interactions, v.v.)
   - Cron job chạy hàng ngày

3. **Độ Chính Xác**: 
   - Test accuracy: 64%
   - Model có thể cần tối ưu hóa với dữ liệu thực tế

## 🔍 Troubleshooting

### Model Không Load
```
Error: Lead Scoring Service not available
```
**Giải pháp**: Kiểm tra xem các file model có tồn tại trong `model AI/` folder

### AI Score Không Cập Nhật
```
Hãy kiểm tra:
1. Cron job có chạy không?
2. Lead có interaction_ids không?
3. Xem log: Settings → Technical → Logs
```

### ImportError
```
Error: ModuleNotFoundError: No module named 'sklearn'
```
**Giải pháp**:
```bash
pip install scikit-learn pandas numpy
```

## 📚 Tài Liệu Tham Khảo

### Features Used
- **Company Size**: ['1-10', '11-50', '51-200', '201-500', '500+']
- **Budget**: Monetary (0-999,999,999)
- **Interactions**: Calls, Emails, Meetings (count)
- **Engagement**: Response rate, Email open rate, Page views
- **Lead Age**: Days since creation
- **Quality**: Manual quality score (0-100)

### Model Algorithm
- **Algorithm**: Gradient Boosting Classifier
- **Framework**: Scikit-learn
- **Hyperparameters**:
  - n_estimators: 100
  - learning_rate: 0.1
  - max_depth: 5

## 🎓 Ví Dụ Sử Dụng

### Lấy Prediction Programmatically

```python
from model_AI import get_lead_scoring_service

service = get_lead_scoring_service()

lead_data = {
    'company_size': '51-200',
    'budget': 500000,
    'num_calls': 5,
    'num_emails': 10,
    'num_meetings': 3,
    'days_since_interaction': 2,
    'response_rate': 0.8,
    'email_open_rate': 0.6,
    'page_views': 50,
    'lead_age_days': 30,
    'priority_score': 3,
    'quality_score': 75
}

result = service.predict_lead_quality(lead_data)
print(f"Conversion Probability: {result['conversion_probability']}%")
print(f"Will Convert: {result['will_convert']}")
print(f"Confidence: {result['confidence']}")
print(f"Risk Level: {result['risk_level']}")
```

## 📞 Hỗ Trợ

Nếu có vấn đề hoặc cần tối ưu hóa model, liên hệ với:
- **AI Team**: AI@BTL.com
- **Technical Support**: Support@BTL.com

---

**Phiên bản**: 1.0.0  
**Cập nhật cuối**: 2026-01-23  
**Trạng thái**: Production Ready ✅
