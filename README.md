# 🤖 Telegram Bot Quản lý Chi tiêu Cá nhân

Bot Telegram tự động để theo dõi chi tiêu cá nhân và lưu trữ dữ liệu vào Google Sheets sử dụng n8n.

## ✨ Tính năng

- 💰 **Thêm chi tiêu nhanh**: Gửi tin nhắn theo định dạng `[số tiền] [mô tả]`
- 📊 **Xem chi tiêu hôm nay**: Sử dụng lệnh `/view`
- 🏷️ **Phân loại tự động**: Bot tự động phân loại chi tiêu theo từ khóa
- 📈 **Thống kê theo danh mục**: Xem tổng chi tiêu theo từng danh mục
- 🔄 **Đồng bộ Google Sheets**: Tự động lưu dữ liệu vào Google Sheets
- 🌍 **Hỗ trợ tiếng Việt**: Giao diện và định dạng theo tiếng Việt

## 🔧 Cài đặt

### 1. Tạo Telegram Bot

1. Mở Telegram và tìm [@BotFather](https://t.me/BotFather)
2. Gửi lệnh `/newbot`
3. Đặt tên cho bot (ví dụ: "Chi Tiêu Bot")
4. Đặt username cho bot (ví dụ: "my_expense_bot")
5. Lưu **Bot Token** được cung cấp

### 2. Tạo Google Sheet

1. Tạo Google Sheet mới tại [sheets.google.com](https://sheets.google.com)
2. Đổi tên sheet thành "Expenses"
3. Thêm header row với các cột:
   ```
   A: Ngày | B: Giờ | C: Số tiền | D: Mô tả | E: Danh mục | F: Người dùng
   ```
4. Lưu **Sheet ID** từ URL (phần sau `/d/` và trước `/edit`)

### 3. Cấu hình n8n

1. **Import workflow**:
   - Mở n8n interface
   - Chọn "Import from File"
   - Upload file `telegram-expense-bot.json`

2. **Cấu hình Telegram credentials**:
   - Tạo credential mới cho Telegram
   - Nhập Bot Token từ BotFather
   - Lưu với tên "Telegram Bot Credentials"

3. **Cấu hình Google Sheets credentials**:
   - Tạo credential mới cho Google Sheets OAuth2
   - Thực hiện OAuth flow với Google account
   - Lưu với tên "Google Sheets Credentials"

4. **Cập nhật Sheet ID**:
   - Mở workflow editor
   - Tìm nodes "Read Google Sheet" và "Save to Google Sheet"
   - Thay `YOUR_GOOGLE_SHEET_ID` bằng Sheet ID thực tế

5. **Kích hoạt workflow**:
   - Bấm "Active" để kích hoạt workflow
   - Webhook sẽ tự động được tạo

## 📱 Cách sử dụng

### Lệnh cơ bản

- `/start` - Bắt đầu sử dụng bot
- `/help` - Xem hướng dẫn chi tiết
- `/view` - Xem chi tiêu hôm nay

### Thêm chi tiêu

Gửi tin nhắn theo định dạng: `[số tiền] [mô tả]`

**Ví dụ:**
```
50000 ăn trưa
25000 cafe sáng
150000 mua sắm quần áo
30000 xăng xe
```

### Phân loại tự động

Bot tự động phân loại chi tiêu dựa trên từ khóa:

- **Ăn uống**: ăn, cafe, uống, trưa, sáng, tối
- **Di chuyển**: xăng, xe, grab, taxi
- **Mua sắm**: mua, shopping, quần áo, giày
- **Sinh hoạt**: điện, nước, nhà, tiền nhà
- **Giải trí**: game, phim, giải trí
- **Khác**: Tất cả các chi tiêu không thuộc danh mục trên

## 📊 Dữ liệu Google Sheets

Cấu trúc dữ liệu được lưu trong Google Sheets:

| Cột | Tên | Mô tả |
|-----|-----|-------|
| A | Ngày | Ngày chi tiêu (dd/mm/yyyy) |
| B | Giờ | Thời gian chi tiêu (hh:mm:ss) |
| C | Số tiền | Số tiền chi tiêu |
| D | Mô tả | Mô tả chi tiêu |
| E | Danh mục | Danh mục tự động |
| F | Người dùng | Tên người dùng Telegram |

## 🔧 Tùy chỉnh

### Thêm danh mục mới

Chỉnh sửa trong node "Parse Expense", section phân loại tự động:

```javascript
if (desc.includes('học') || desc.includes('sách') || desc.includes('khóa học')) {
  category = 'Học tập';
}
```

### Thay đổi định dạng tin nhắn

Chỉnh sửa text trong các nodes "Send..." để thay đổi nội dung tin nhắn.

### Thêm lệnh mới

1. Thêm node "If" mới để kiểm tra lệnh
2. Thêm logic xử lý tương ứng
3. Kết nối với Telegram Webhook

## 🚨 Lỗi thường gặp

### Bot không phản hồi
- Kiểm tra Bot Token có đúng không
- Đảm bảo workflow đã được kích hoạt
- Kiểm tra webhook URL trong Telegram settings

### Lỗi Google Sheets
- Kiểm tra credentials Google Sheets
- Đảm bảo Sheet ID đúng
- Kiểm tra quyền truy cập Google Sheet

### Định dạng chi tiêu không đúng
- Đảm bảo có khoảng trắng giữa số tiền và mô tả
- Số tiền phải là số nguyên hoặc thập phân
- Mô tả không được để trống

## 🔒 Bảo mật

- Bot Token và Google credentials được mã hóa trong n8n
- Chỉ người dùng có quyền truy cập n8n mới có thể xem/chỉnh sửa
- Google Sheets có thể được bảo vệ bằng quyền truy cập riêng tư

## 📞 Hỗ trợ

Nếu gặp vấn đề, hãy kiểm tra:

1. **Logs trong n8n**: Xem execution history để debug
2. **Test workflow**: Sử dụng manual execution để test từng node
3. **Telegram webhook**: Kiểm tra webhook status trong Bot settings

## 📝 Ghi chú

- Bot lưu múi giờ Việt Nam (UTC+7)
- Dữ liệu được lưu realtime vào Google Sheets
- Không giới hạn số lượng chi tiêu mỗi ngày
- Hỗ trợ nhiều người dùng cùng lúc (nếu cấu hình đúng)

---

**Phiên bản**: 1.0  
**Tác giả**: n8n Automation  
**Cập nhật**: {{ new Date().toLocaleDateString('vi-VN') }}