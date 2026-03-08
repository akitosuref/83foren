# Hướng Dẫn Cấu Hình Firebase cho Website Tình Yêu

## Bước 1: Tạo Project Firebase (MIỄN PHÍ)

1. Truy cập: https://console.firebase.google.com/
2. Click "Add project" hoặc "Thêm dự án"
3. Đặt tên project (ví dụ: "love-website-83")
4. Disable Google Analytics (không cần thiết)
5. Click "Create project"

## Bước 2: Tạo Realtime Database

1. Trong Firebase Console, chọn "Realtime Database" ở menu bên trái
2. Click "Create Database"
3. Chọn vị trí: **asia-southeast1** (gần Việt Nam nhất)
4. Chọn chế độ: **"Start in test mode"** (cho phép đọc/ghi trong 30 ngày)
5. Click "Enable"

## Bước 3: Lấy Configuration Code

1. Click vào biểu tượng ⚙️ (Settings) > "Project settings"
2. Scroll xuống phần "Your apps"
3. Click vào biểu tượng Web "</>" để thêm web app
4. Đặt tên app (ví dụ: "love-website")
5. Click "Register app"
6. Copy đoạn code `firebaseConfig`

## Bước 4: Cập Nhật Code Trong index.html

Mở file `index.html`, tìm đoạn code (khoảng dòng 10-20):

```javascript
const firebaseConfig = {
    apiKey: "AIzaSyDemoKey-ReplaceWithYourKey",  // ⬅️ THAY ĐỔI
    authDomain: "love-website-demo.firebaseapp.com",  // ⬅️ THAY ĐỔI
    databaseURL: "https://love-website-demo-default-rtdb.firebaseio.com",  // ⬅️ THAY ĐỔI
    projectId: "love-website-demo",  // ⬅️ THAY ĐỔI
    storageBucket: "love-website-demo.appspot.com",  // ⬅️ THAY ĐỔI
    messagingSenderId: "123456789",  // ⬅️ THAY ĐỔI
    appId: "1:123456789:web:abcdef123456"  // ⬅️ THAY ĐỔI
};
```

Thay thế bằng config từ Firebase Console của bạn.

## Bước 5: Cấu Hình Security Rules (QUAN TRỌNG!)

1. Vào "Realtime Database" > tab "Rules"
2. Thay thế rules hiện tại bằng:

```json
{
  "rules": {
    "loveMessages": {
      ".read": true,
      ".write": true,
      "$messageId": {
        ".validate": "newData.hasChildren(['name', 'msg', 'date', 'timestamp'])"
      }
    }
  }
}
```

3. Click "Publish"

**Lưu ý bảo mật:**
- Rules trên cho phép mọi người đọc/ghi
- Để bảo mật hơn (sau này), bạn có thể giới hạn số lần ghi hoặc thêm xác thực

## Bước 6: Test

1. Mở website của bạn
2. Thử gửi một lời yêu thương
3. Kiểm tra trong Firebase Console > Realtime Database > Data
4. Bạn sẽ thấy dữ liệu xuất hiện!

## Bước 7: Deploy lên GitHub + Vercel

Sau khi cập nhật config:
```bash
git add .
git commit -m "Add Firebase Realtime Database for love messages"
git push origin main
```

Vercel sẽ tự động deploy và website của bạn sẽ hoạt động với database thật!

## Giới Hạn Miễn Phí Firebase

- **Spark Plan (FREE):**
  - 1GB dữ liệu lưu trữ
  - 10GB/tháng bandwidth
  - 100 kết nối đồng thời
  
Với website tình yêu cá nhân, giới hạn này **quá đủ**!

## Troubleshooting

### Lỗi: "Permission denied"
- Kiểm tra lại Security Rules
- Đảm bảo databaseURL đúng

### Lỗi: "Firebase not initialized"  
- Kiểm tra lại firebaseConfig
- Đảm bảo không có lỗi trong Console (F12)

### Tin nhắn không hiển thị
- Mở F12 Console để xem lỗi
- Kiểm tra Network tab xem có call đến Firebase không

## Hỗ Trợ

Nếu gặp khó khăn, check:
1. Firebase Console > Realtime Database > Data (xem có data không)
2. Browser Console (F12) > Console tab (xem có lỗi gì)
3. Firebase Console > Realtime Database > Usage (xem có request nào không)

---

**Chúc bạn thành công! ❤️**
