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

## 🔄 Quy trình Cập nhật Tự động (Update Pipeline)

Quy trình xử lý được chia làm **4 giai đoạn chính** nhằm bảo đảm không gây đơ giao diện (UI Freeze) và an toàn dữ liệu:

| Giai đoạn | Hành động chính | Chi tiết kỹ thuật |
| :--- | :--- | :--- |
| **1. Check Phase** *(Bất đồng bộ)* | 🔍 **Kiểm tra phiên bản** | - Gửi GET Request tới GitHub REST API.<br>- Parse chuỗi Tag Version theo chuẩn `SemVer` (Semantic Versioning). |
| **2. Decision Phase** *(User Interaction)* | 🎨 **Tương tác Giao diện** | - So sánh Version hiện tại với `latest_release`.<br>- Hiển thị Form WinForms render nội dung Release Notes dạng Markdown.<br>- Người dùng lựa chọn **Cập nhật ngay** hoặc **Bỏ qua**. |
| **3. Download Phase** *(Temp Storage)* | 📥 **Tải gói cập nhật** | - Tải file nén `.zip` đính kèm từ GitHub Asset về `%TEMP%/AutoUpdate/`.<br>- Báo tiến trình liên tục qua `IProgress<int>` lên thanh Progress Bar. |
| **4. Apply Phase** *(Independent Process)* | 🔄 **Ghi đè & Re-launch** | - Gọi `Updater.exe` riêng biệt và đóng App chính.<br>- Sau khi App chính giải phóng File Lock: Sao lưu (Backup) $\rightarrow$ Ghi đè File $\rightarrow$ Khởi chạy lại App chính. |n giải nén đè file mới.
- <img src="https://img.shields.io/badge/Step_6-Hoàn_tất-brightgreen?style=for-the-badge" height="22"/> **Re-launch:** Tự động mở lại ứng dụng chính và xóa các file tạm (`Clean Temp`).
