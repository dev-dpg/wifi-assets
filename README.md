# Image Hosting Repo

Repo này dùng để host ảnh tĩnh trên **GitHub Pages** và lấy link cố định để sử dụng.

## Cách hoạt động
- Ảnh được lưu trong thư mục `brands/`.
- Khi đẩy lên GitHub, GitHub Pages sẽ cung cấp link cố định cho ảnh:
https://<username>.github.io/<repo-name>/brands/apple/iphone.png

css
Sao chép mã
- Chỉ cần thay ảnh trong repo rồi commit + push, link sẽ tự động cập nhật.

## Cấu trúc thư mục
image-hosting-repo/
├── brands/
│ ├── apple/
│ ├── samsung/
│ └── xiaomi/
└── README.md

bash
Sao chép mã

## Cách upload / replace / tạo mới thư mục bằng Git command

### 1. Clone repo về máy
```bash
git clone https://github.com/<username>/<repo-name>.git
cd <repo-name>
2. Thêm ảnh hoặc thay ảnh
Copy ảnh mới vào thư mục brands/<brand-name>/.

3. Tạo thư mục brand mới (ví dụ: oppo)
bash
Sao chép mã
mkdir brands/oppo
cp ~/Downloads/oppo1.png brands/oppo/
4. Commit và push thay đổi
bash
Sao chép mã
git add .
git commit -m "update images"
git push origin main
5. Truy cập link ảnh
Sau khi push, ảnh sẽ có link cố định:

php-template
Sao chép mã
https://<username>.github.io/<repo-name>/brands/<brand-name>/<image-name>.png
