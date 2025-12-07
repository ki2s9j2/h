# 📧 Hướng Dẫn Sử Dụng API Notification

## 🎯 Mục đích

API này nhận thông báo từ web tỏ tình (`https://bat-ngo-bvno.vercel.app/`) và gửi email/webhook cho bạn.

## 🚀 Các bước deploy

### Bước 1: Upload code lên GitHub

1. Tạo repository mới trên GitHub (ví dụ: `totinh-api`)
2. Upload tất cả file trong thư mục `totinh-api` lên GitHub:
   - `api/notify.js`
   - `package.json`
   - `README.md`

### Bước 2: Deploy lên Vercel

1. Vào [Vercel Dashboard](https://vercel.com/dashboard)
2. Click **"Add New"** → **"Project"**
3. Import repository `totinh-api` từ GitHub
4. Click **"Deploy"**
5. Đợi deploy xong (30-60 giây)

### Bước 3: Lấy API URL

Sau khi deploy xong, Vercel sẽ cho bạn link:
```
https://[tên-project].vercel.app
```

API endpoint sẽ là:
```
https://[tên-project].vercel.app/api/notify
```

**Ví dụ:** `https://totinh-api.vercel.app/api/notify`

### Bước 4: Cập nhật CORS (nếu cần)

Nếu web tỏ tình của bạn chạy ở domain khác, sửa file `api/notify.js`:

Tìm dòng:
```javascript
const allowedOrigins = [
  'https://bat-ngo-bvno.vercel.app',
  ...
];
```

Thêm domain của bạn vào:
```javascript
const allowedOrigins = [
  'https://bat-ngo-bvno.vercel.app',  // Web tỏ tình hiện tại
  'https://your-new-domain.com',       // Thêm domain mới
  'http://localhost:3000',
  'http://localhost:5500'
];
```

### Bước 5: Cập nhật script.js của web tỏ tình

1. Mở file `script.js` của web tỏ tình
2. Tìm dòng:
```javascript
const API_URL = ''; // 👈 ĐIỀN API URL CỦA BẠN VÀO ĐÂY
```
3. Điền API URL của bạn:
```javascript
const API_URL = 'https://totinh-api.vercel.app/api/notify';
```
4. Lưu và deploy lại web tỏ tình

## 📧 Setup Email Notification (Tùy chọn)

Nếu muốn nhận email khi có thông báo:

### Dùng Resend (Miễn phí 3000 email/tháng)

1. Đăng ký tại [resend.com](https://resend.com)
2. Tạo API Key
3. Vào Vercel Dashboard → Project → Settings → Environment Variables
4. Thêm các biến sau:
   ```
   EMAIL_SERVICE=resend
   EMAIL_API_KEY=re_xxxxxxxxxxxxx
   EMAIL_FROM=noreply@yourdomain.com
   EMAIL_TO=your-email@gmail.com
   ```
5. Redeploy project

## 🔔 Setup Webhook (Tùy chọn)

Nếu muốn gửi thông báo đến Discord/Slack/Telegram:

1. Tạo webhook URL (ví dụ: Discord webhook)
2. Vào Vercel Dashboard → Settings → Environment Variables
3. Thêm:
   ```
   WEBHOOK_URL=https://discord.com/api/webhooks/xxxxx/xxxxx
   ```
4. Redeploy project

## 📊 Xem Logs

1. Vào [Vercel Dashboard](https://vercel.com/dashboard)
2. Chọn project `totinh-api`
3. Vào tab **"Functions"** hoặc **"Logs"**
4. Xem real-time logs khi có người tương tác

## ✅ Test API

Sau khi deploy, test bằng cách:

1. Mở web tỏ tình: `https://bat-ngo-bvno.vercel.app/`
2. Bấm các nút (Start, Đồng ý, Không)
3. Vào Vercel Dashboard → Functions → Logs để xem thông báo

Hoặc dùng curl:
```bash
curl -X POST https://your-api.vercel.app/api/notify \
  -H "Content-Type: application/json" \
  -H "Origin: https://bat-ngo-bvno.vercel.app" \
  -d '{
    "action": "yes",
    "eventType": "click",
    "timestamp": "2024-12-25T10:30:00Z",
    "userAgent": "Mozilla/5.0...",
    "isMobile": false
  }'
```

## 🎉 Xong!

Bây giờ bạn sẽ nhận thông báo mỗi khi có người tương tác với web tỏ tình!


