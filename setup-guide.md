# 🚀 Hướng dẫn Cài đặt Nhanh

## Bước 1: Tạo Telegram Bot (5 phút)

1. Mở Telegram, tìm [@BotFather](https://t.me/BotFather)
2. Gửi: `/newbot`
3. Đặt tên bot: `Chi Tiêu Bot`
4. Đặt username: `your_expense_bot` (phải unique)
5. **Lưu Bot Token** (dạng: `123456789:ABCdefGHIjklMNOpqrsTUVwxyz`)

## Bước 2: Tạo Google Sheet (3 phút)

1. Vào [sheets.google.com](https://sheets.google.com)
2. Tạo sheet mới
3. Đổi tên sheet thành: `Expenses`
4. Copy header này vào dòng 1:
   ```
   Ngày	Giờ	Số tiền	Mô tả	Danh mục	Người dùng
   ```
5. **Lưu Sheet ID** từ URL (phần giữa `/d/` và `/edit`)
   - URL: `https://docs.google.com/spreadsheets/d/SHEET_ID_HERE/edit`

## Bước 3: Cấu hình n8n (10 phút)

1. **Import workflow**:
   - Mở n8n
   - Chọn "Import from File"
   - Upload `telegram-expense-bot.json`

2. **Thêm Telegram credential**:
   - Credentials → Add Credential
   - Chọn "Telegram API"
   - Access Token: `[Bot Token từ BotFather]`
   - Lưu tên: "Telegram Bot Credentials"

3. **Thêm Google Sheets credential**:
   - Credentials → Add Credential  
   - Chọn "Google Sheets OAuth2 API"
   - Thực hiện OAuth với Google account
   - Lưu tên: "Google Sheets Credentials"

4. **Cập nhật Sheet ID**:
   - Mở workflow editor
   - Tìm node "Read Google Sheet"
   - Thay `YOUR_GOOGLE_SHEET_ID` → Sheet ID thực tế
   - Tìm node "Save to Google Sheet"  
   - Thay `YOUR_GOOGLE_SHEET_ID` → Sheet ID thực tế

5. **Kích hoạt**:
   - Bấm nút "Active" 
   - Workflow sẽ chạy!

## Bước 4: Test Bot (2 phút)

1. Tìm bot trên Telegram (username bạn đã tạo)
2. Gửi: `/start`
3. Thử thêm chi tiêu: `50000 ăn trưa`
4. Kiểm tra Google Sheet → dữ liệu đã xuất hiện!

## ✅ Checklist hoàn thành

- [ ] Bot Token từ BotFather
- [ ] Google Sheet với header đúng
- [ ] Sheet ID đã copy
- [ ] n8n workflow imported
- [ ] Telegram credential configured
- [ ] Google Sheets credential configured  
- [ ] Sheet ID updated trong workflow
- [ ] Workflow activated
- [ ] Test bot thành công

## 🆘 Nếu có lỗi

1. **Bot không trả lời**: Kiểm tra Bot Token và workflow active
2. **Lỗi Google Sheets**: Kiểm tra Sheet ID và credentials
3. **Lỗi parsing**: Đảm bảo định dạng `[số] [mô tả]`

## 📞 Commands để test

```
/start           → Tin nhắn chào mừng
/help            → Hướng dẫn sử dụng  
/view            → Xem chi tiêu hôm nay
25000 cafe       → Thêm chi tiêu
100000 mua sắm   → Thêm chi tiêu
```

**Thời gian setup**: ~20 phút  
**Skill cần**: Cơ bản (copy/paste, follow hướng dẫn)