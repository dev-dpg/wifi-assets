# Image Hosting Repo

Repo này dùng để host ảnh tĩnh trên **GitHub Pages** và lấy link cố định để sử dụng.

## Cách hoạt động
- Ảnh được lưu trong thư mục `brands/`.
- Khi đẩy lên GitHub, GitHub Pages sẽ cung cấp link cố định cho ảnh:
https://<username>.github.io/<repo-name>/brands/apple/iphone.png


- Chỉ cần thay ảnh trong repo rồi commit + push, link sẽ tự động cập nhật.

## Cấu trúc thư mục
image-hosting-repo/
├── brands/
│ ├── apple/
│ ├── samsung/
│ └── xiaomi/
└── README.md


## Cách upload / replace / tạo mới thư mục bằng Git command

### 1. Clone repo về máy
git clone https://github.com/<username>/<repo-name>.git
cd <repo-name>

2. Thêm ảnh hoặc thay ảnh
Copy ảnh mới vào thư mục brands/<brand-name>/.

3. Tạo thư mục brand mới (ví dụ: oppo)

mkdir brands/oppo
cp ~/Downloads/oppo1.png brands/oppo/

4. Commit và push thay đổi
git add .
git commit -m "update images"
git push origin main
5. Truy cập link ảnh
Sau khi push, ảnh sẽ có link cố định:
https://<username>.github.io/<repo-name>/brands/<brand-name>/<image-name>.png

# Quản lý và cập nhật brands.json

Repo này dùng để lưu trữ file `brands.json` và phục vụ trực tiếp qua **GitHub Pages**.  
Mục đích: cho phép frontend fetch dữ liệu JSON từ link tĩnh, nhưng vẫn có thể chỉnh sửa file thông qua **GitHub Issues** mà không cần backend.

---

## Cấu trúc thư mục

```
brands/brands.json
.github/workflows/update-brands.yml
```

---

## Luồng hoạt động

1. Frontend fetch dữ liệu từ:

   ```
   https://<username>.github.io/<repo>/brands/brands.json
   ```

2. Khi cần chỉnh sửa, người quản trị tạo một **Issue** trong repo.

3. **GitHub Actions** (được định nghĩa trong `.github/workflows/update-brands.yml`) sẽ chạy khi Issue có tiêu đề phù hợp:
   - Action đọc nội dung JSON trong body của Issue  
   - Action ghi đè vào `brands/brands.json`  
   - Action commit và push trực tiếp vào nhánh `main`  
   - GitHub Pages tự động build lại và phục vụ bản JSON mới  

---

## Cách update brands.json

1. Vào tab **Issues** của repo  
2. Tạo Issue mới  
   - **Tiêu đề:** `Update brands.json`  
   - **Nội dung:** paste toàn bộ JSON muốn thay thế.  

   Ví dụ:

   ```json
   {
     "Brands": [
       {
         "BrandName": "Apple",
         "Config": { "Status": true },
         "Campaigns": []
       }
     ]
   }
   ```

3. Nhấn **Create Issue**  
4. Sau khoảng 30-60 giây, GitHub Actions sẽ commit thay đổi  
5. Truy cập lại link GitHub Pages để thấy bản cập nhật:

   ```
   https://<username>.github.io/<repo>/brands/brands.json
   ```

---

## Lưu ý

- JSON trong Issue phải hợp lệ, nếu không Action sẽ lỗi và không commit  
- Chỉ người có quyền mở Issue trong repo mới có thể cập nhật file  
- Có thể giới hạn user được phép cập nhật bằng cách chỉnh điều kiện trong workflow (kiểm tra `github.actor`)  
- Quá trình cập nhật có độ trễ ngắn (do GitHub Actions và Pages cần vài chục giây để chạy)  

---
