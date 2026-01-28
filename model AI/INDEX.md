# 📚 Predictive Lead Scoring - Documentation Index

## 📖 Hướng Dẫn Nhanh

Chọn mục dựa trên nhu cầu của bạn:

### 🚀 Tôi muốn bắt đầu ngay (5 phút)
👉 **→ Đọc: [QUICK_START.md](QUICK_START.md)**
- Xác nhận model hoạt động
- Mở Odoo và xem AI score
- Hiểu kết quả dự đoán

### 📚 Tôi cần hướng dẫn chi tiết
👉 **→ Đọc: [PREDICTIVE_LEAD_SCORING_GUIDE.md](PREDICTIVE_LEAD_SCORING_GUIDE.md)**
- Tính năng chính
- Kết quả huấn luyện
- Cấu trúc file
- Cách sử dụng
- Troubleshooting

### 🔧 Tôi cần thông tin kỹ thuật
👉 **→ Đọc: [IMPLEMENTATION_SUMMARY.md](IMPLEMENTATION_SUMMARY.md)**
- Kiến trúc hệ thống
- Workflow dự đoán
- Mục tiêu đạt được
- File được tạo/sửa

### 📋 Tôi cần tóm tắt toàn bộ
👉 **→ Đọc: [README_FINAL.md](README_FINAL.md)**
- Tóm tắt công việc hoàn thành
- Cách hoạt động
- Lợi ích
- Test ngay

---

## 🎯 Các Tình Huống Sử Dụng

### Tình Huống 1: Mở Lead và Xem AI Score

```
1. Mở Odoo: http://localhost:8069
2. Vào: CRM → Leads
3. Chọn một Lead
4. Scroll xuống xem "AI Scoring" section
5. Xem: ai_score, ai_will_convert, ai_confidence, ai_risk_level
```

📖 **Tham khảo**: QUICK_START.md

### Tình Huống 2: Cập Nhật AI Score Thủ Công

```
1. Mở Lead
2. Nhấn nút "Refresh AI Score"
3. AI score sẽ cập nhật ngay
4. Xem kết quả mới
```

📖 **Tham khảo**: PREDICTIVE_LEAD_SCORING_GUIDE.md (Cách Sử Dụng)

### Tình Huống 3: Ưu Tiên Hóa Lead

```
1. Xem ai_score của leads
2. Focus vào leads có score ≥ 80%
3. Follow-up nhanh
4. Tăng tỷ lệ chuyển đổi
```

📖 **Tham khảo**: PREDICTIVE_LEAD_SCORING_GUIDE.md (Giải Thích AI Score)

### Tình Huống 4: Huấn Luyện Lại Model

```
1. Export dữ liệu leads thực từ Odoo
2. Chạy: python model_AI/predictive_lead_scoring_trainer.py
3. Lưu model mới
4. Restart Odoo
```

📖 **Tham khảo**: PREDICTIVE_LEAD_SCORING_GUIDE.md (Tùy Chỉnh Model)

### Tình Huống 5: Troubleshooting

```
1. AI score không hiển thị?
2. Lỗi import model?
3. Model trả về default score?
4. Xem phần "Troubleshooting"
```

📖 **Tham khảo**: PREDICTIVE_LEAD_SCORING_GUIDE.md (Troubleshooting)

---

## 📂 Cấu Trúc Thư Mục

```
custom-addons/
│
├── model AI/
│   ├── 📖 README_FINAL.md ..................... Tóm tắt toàn bộ
│   ├── 📖 QUICK_START.md ..................... Bắt đầu nhanh
│   ├── 📖 PREDICTIVE_LEAD_SCORING_GUIDE.md ... Hướng dẫn chi tiết
│   ├── 📖 IMPLEMENTATION_SUMMARY.md .......... Tóm tắt kỹ thuật
│   ├── 📄 INDEX.md (file này) ................ Chỉ mục tài liệu
│   │
│   ├── 🐍 lead_scoring_service.py ........... Service dự đoán
│   ├── 🐍 predictive_lead_scoring_trainer.py  Script huấn luyện
│   ├── 🐍 __init__.py ....................... Package init
│   │
│   ├── 📦 lead_scoring_model.pkl ............ Mô hình ML
│   ├── 📦 lead_scoring_model_scaler.pkl .... StandardScaler
│   ├── 📦 lead_scoring_model_encoders.pkl .. LabelEncoder
│   ├── 📦 lead_scoring_model_features.pkl .. Feature names
│   │
│   └── 📁 dataset/ .......................... Thư mục dataset
│
├── BTL_Quan_ly_khach_hang/
│   └── models/
│       └── crm_lead.py (✅ Đã cập nhật với AI fields & methods)
│
├── BTL_AI_Customer_Intelligence/
│   └── ... (AI module chính)
│
└── ... (other modules)
```

---

## 🔍 Tìm Kiếm Nhanh

### Muốn tìm thông tin về:

| Chủ Đề | Trang |
|--------|------|
| **Algorithm** | PREDICTIVE_LEAD_SCORING_GUIDE.md → "Model Algorithm" |
| **Features** | PREDICTIVE_LEAD_SCORING_GUIDE.md → "Features Sử Dụng" |
| **Kết quả huấn luyện** | README_FINAL.md → "KẾT QUẢ HUẤN LUYỆN" |
| **Cách sử dụng** | QUICK_START.md → "5 Phút để Bắt Đầu" |
| **Tích hợp Odoo** | IMPLEMENTATION_SUMMARY.md → "Các Field mới" |
| **Troubleshooting** | PREDICTIVE_LEAD_SCORING_GUIDE.md → "Troubleshooting" |
| **Giải thích score** | PREDICTIVE_LEAD_SCORING_GUIDE.md → "Giải Thích AI Score" |
| **Code** | lead_scoring_service.py & predictive_lead_scoring_trainer.py |

---

## 📞 FAQ - Câu Hỏi Thường Gặp

### Q: Model ở đâu?
**A**: Tại `model AI/lead_scoring_model.pkl` (0.36 MB)

### Q: Làm sao xem AI score?
**A**: Mở Lead trong Odoo → Scroll xuống xem "AI Scoring" section

### Q: Làm sao cập nhật AI score?
**A**: Nhấn nút "Refresh AI Score" trong Lead form

### Q: Mô hình học cái gì?
**A**: 15 features về lead (budget, interactions, engagement, v.v.)

### Q: Độ chính xác là bao nhiêu?
**A**: 64% trên test set (có thể cải thiện với dữ liệu thực)

### Q: Muốn huấn luyện lại mô hình?
**A**: Xem PREDICTIVE_LEAD_SCORING_GUIDE.md → "Tùy Chỉnh Model"

### Q: Model có tự động cập nhật không?
**A**: Có, hàng ngày qua cron job (02:00 AM)

### Q: Nếu model không load?
**A**: Xem PREDICTIVE_LEAD_SCORING_GUIDE.md → "Troubleshooting"

---

## ✅ Danh Sách Kiểm Tra

Trước khi sử dụng, hãy đảm bảo:

- [ ] Odoo đã được restart
- [ ] Model files tồn tại (4 .pkl files)
- [ ] BTL_Quan_ly_khach_hang module đã install
- [ ] Có ít nhất 1 lead trong hệ thống
- [ ] Xem được "AI Scoring" section trong Lead form

---

## 🎓 Các Bước Tiếp Theo

### Tuần 1:
- [ ] Test AI scoring trên 10 leads
- [ ] Kiểm tra độ chính xác
- [ ] Feedback từ nhân viên

### Tuần 2-4:
- [ ] Thu thập dữ liệu thực
- [ ] Huấn luyện lại model
- [ ] Deploy model mới

### Tháng 2:
- [ ] Tích hợp thêm features
- [ ] Thêm sentiment analysis
- [ ] Phân tích ROI

---

## 🌐 Liên Kết Hữu Ích

- **Scikit-learn**: https://scikit-learn.org/
- **Odoo Documentation**: https://www.odoo.com/documentation
- **Pandas**: https://pandas.pydata.org/
- **NumPy**: https://numpy.org/

---

## 📝 Ghi Chú

- **Phiên bản**: 1.0.0
- **Cập nhật cuối**: 2026-01-23
- **Trạng thái**: Production Ready ✅
- **Hỗ trợ**: Tiếng Việt 🇻🇳

---

## 🎉 Bắt Đầu Ngay

👉 **Chọn một tài liệu để bắt đầu**:

1. **QUICK_START.md** - Nhanh nhất (5 phút) ⚡
2. **PREDICTIVE_LEAD_SCORING_GUIDE.md** - Chi tiết (30 phút) 📚
3. **IMPLEMENTATION_SUMMARY.md** - Kỹ thuật (15 phút) 🔧
4. **README_FINAL.md** - Tóm tắt (10 phút) 📋

---

**Chúc bạn thành công! 🚀**
