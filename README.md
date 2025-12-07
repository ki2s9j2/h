# 📧 API Notification Service

API riêng để nhận thông báo từ web tỏ tình.

## 🚀 Deploy lên Vercel

### Bước 1: Tạo repository trên GitHub

1. Tạo repository mới trên GitHub (ví dụ: `totinh-api`)
2. Upload tất cả file trong thư mục này lên GitHub

### Bước 2: Deploy lên Vercel

1. Vào [Vercel Dashboard](https://vercel.com/dashboard)
2. Click **"Add New"** → **"Project"**
3. Import repository `totinh-api` từ GitHub
4. Click **"Deploy"**
5. Đợi deploy xong, bạn sẽ có link: `https://totinh-api.vercel.app` (hoặc tên khác)

### Bước 3: Lấy API URL

Sau khi deploy xong, API URL sẽ là:
```
https://[tên-project].vercel.app/api/notify
```

Ví dụ: `https://totinh-api.vercel.app/api/notify`

### Bước 4: Cập nhật CORS (nếu cần)

Nếu web tỏ tình của bạn chạy ở domain khác, sửa file `api/notify.js`:

```javascript
const allowedOrigins = [
  'https://bat-ngo-bvno.vercel.app',  // Web tỏ tình của bạn
  'https://your-other-domain.com',    // Thêm domain khác nếu có
  'http://localhost:3000',
  'http://localhost:5500'
];
```

### Bước 5: Setup Environment Variables (Tùy chọn)

Nếu muốn nhận email/webhook, vào Vercel Dashboard → Settings → Environment Variables:

**Email (Resend):**
```
EMAIL_SERVICE=resend
EMAIL_API_KEY=re_xxxxxxxxxxxxx
EMAIL_FROM=noreply@yourdomain.com
EMAIL_TO=your-email@gmail.com
```

**Webhook:**
```
WEBHOOK_URL=https://discord.com/api/webhooks/xxxxx/xxxxx
```

## 📱 Test API

Sau khi deploy, test API bằng cách:

1. Mở Postman hoặc dùng curl:
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

2. Vào Vercel Dashboard → Functions → Logs để xem thông báo

## ✅ Xong!

Copy API URL và cập nhật vào file `script.js` của web tỏ tình.


