# PHP Đồng Hồ

Bộ khởi tạo Laravel API + React/Vite cho nhóm phát triển website bán đồng hồ. Chưa triển khai chức năng nghiệp vụ hoặc dữ liệu mẫu.

## Cấu trúc

- `backend/`: Laravel, cấu hình ứng dụng và migration mặc định cho users, cache, jobs.
- `frontend/`: React + Vite, trang khởi tạo và proxy `/api` tới Laravel.

## Yêu cầu

PHP 8.4.1+, Composer 2, Node.js 20.19+ hoặc 22.12+, MySQL.

## Chạy backend

```powershell
cd backend
composer install
if (-not (Test-Path .env)) {
    Copy-Item .env.example .env
    php artisan key:generate
}
php artisan serve --host=127.0.0.1 --port=8000
```

Nếu máy chưa có lệnh `composer`, dùng `php F:\ComposerSetup\composer.phar install`.

Giữ nguyên `.env` và `APP_KEY` nếu đã có. Khi cần database, tạo database mới, cấu hình `DB_*` trong `.env`, rồi chạy `php artisan migrate`. Repo chỉ chứa migration khởi tạo; nhóm sẽ tự xây dựng schema nghiệp vụ. Không chạy `migrate:fresh` trên database đang có dữ liệu.

API kiểm tra: `http://127.0.0.1:8000/api/health`.

## Chạy frontend

Mở terminal thứ hai:

```powershell
cd frontend
npm.cmd ci
npm.cmd run dev -- --host 127.0.0.1
```

Mở `http://127.0.0.1:5173`. Vite chuyển các request `/api` tới `http://127.0.0.1:8000`; có thể đổi bằng `DEV_API_TARGET` trong `frontend/.env.local`.

## Kiểm tra frontend

```powershell
cd frontend
npm.cmd run lint
npm.cmd run build
```

File `.env`, chứng chỉ và thư mục dependency không được đưa lên Git.
