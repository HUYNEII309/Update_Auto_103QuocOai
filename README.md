# 🚀 AutoUpdater.GitHub (WinForms C#)

[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)](https://github.com/)
[![Platform](https://img.shields.io/badge/platform-WinForms%20%7C%20.NET%20Framework%204.8%2B%20%7C%20.NET%208.0%2B-blue.svg)](https://dotnet.microsoft.com/)
[![GitHub Release](https://img.shields.io/github/v/release/your-username/your-repo-name?color=orange)](https://github.com/your-username/your-repo-name/releases)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

Giải pháp tự động kiểm tra và cập nhật phiên bản mới nhất cho ứng dụng **Windows Forms (C#)** trực tiếp từ **GitHub Releases**. Tích hợp nhanh chóng, giao diện mượt mà, hỗ trợ tải file ngầm và tự động khởi động lại ứng dụng.

---

## 📌 Tính năng nổi bật (Features)

- 🔍 **Kiểm tra phiên bản tự động:** Gọi GitHub REST API để so sánh `Semantic Versioning` (ví dụ: `v1.0.0` vs `v1.0.1`).
- 🎨 **Giao diện WinForms tích hợp:** Hiển thị thông báo `Release Notes` (Markdown support) và thanh tiến trình `ProgressBar` tải về.
- 📦 **Tự động giải nén & ghi đè:** Hỗ trợ file nén `.zip` hoặc file cài đặt `.exe`/`.msi`.
- 🛡️ **Sao lưu & Rollback:** Tự động backup phiên bản cũ trước khi đè file mới, tránh lỗi xẩy ra giữa chừng.
- 🔄 **Khởi động lại tự động:** Chạy quy trình updater độc lập bằng process riêng (`Updater.exe`) để bypass việc khóa file executable đang chạy.
- 🚀 **Bất đồng bộ (Async/Await):** Không gây freeze/treo UI WinForms trong quá trình kiểm tra và download.

---

## 🔄 Luồng hoạt động (Workflow)

```mermaid
graph TD
    A[Ứng dụng WinForms Khởi chạy] --> B[Gọi GitHub API lấy Latest Release]
    B --> C{Có phiên bản mới?}
    C -- Không --> D[Tiếp tục chạy ứng dụng]
    C -- Có --> E[Hiển thị UI Cập nhật & Release Notes]
    E --> F{Nguời dùng đồng ý?}
    F -- Hủy --> D
    F -- Cập nhật --> G[Tải file Release về thư mục Temp]
    G --> H[Khởi chạy Updater.exe & Đóng App chính]
    H --> I[Updater ghi đè file cũ & Chạy lại App chính]
