# Bài 4: Tích hợp CI/CD tự động Pull Image từ GHCR

## Các điểm đã chuẩn hóa trong `.github/workflows/ci.yml`
1. **Phân quyền Token (`permissions`):** Khai báo `packages: read` để `secrets.GITHUB_TOKEN` có quyền đọc/kéo package từ GHCR.
2. **Đăng nhập tự động:** Dùng `docker/login-action@v3` với `username: ${{ github.actor }}` và `password: ${{ secrets.GITHUB_TOKEN }}`.
3. **Chuẩn hóa chữ thường:** Đưa tên owner/image về chữ thường (`tr '[:upper:]' '[:lower:]'`) vì GHCR không chấp nhận chữ hoa trong đường dẫn image.
4. **Pull & Verify tốc độ cao (< 20s):** Kéo trực tiếp `ghcr.io/<owner>/payment-service:1.0.0`, chạy nền (`-d`), kiểm tra trạng thái `docker ps` và dọn dẹp container.
