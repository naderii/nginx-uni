# 🛡️ Nginx امن با Docker
این پروژه برای درس امنیت وب خانم مهندس ربانی ایجاد شده است.
یک پیکربندی امن و بهینه شده از Nginx در محیط Docker با تمرکز بر امنیت و بهترین روش‌ها.

## ✨ ویژگی‌های کلیدی

- 🔒 عدم نمایش نسخه Nginx و سیستم عامل
- 🚫 جلوگیری از دسترسی به دایرکتوری‌ها
- 🛡️ هدرهای امنیتی پیشرفته
- 📁 مسدودسازی دسترسی به فایل‌های حساس
- 🐳 آماده برای اجرا با Docker Compose
- 🔄 راه‌اندازی خودکار پس از توقف غیرمنتظره

## 🚀 راه‌اندازی سریع

1. ابتدا مطمئن شوید Docker و Docker Compose نصب شده‌اند:
   ```bash
   docker --version
   docker-compose --version
   ```
2. پروژه را کلون کنید:
```bash
git clone https://github.com/naderii/nginx-uni.git
cd secure-nginx-docker
```
3. سرویس را اجرا کنید:
```bash
docker-compose up -d
```

## 🛠️ ساختار پروژه
```bash
secure-nginx-docker/
├── docker-compose.yml
├── nginx/
│   ├── nginx.conf          # تنظیمات اصلی Nginx
│   ├── conf.d/
│   │   └── default.conf    # تنظیمات سرور مجازی
│   ├── html/
│   │   └── index.html      # صفحه پیش‌فرض
│   └── logs/               # دایرکتوری لاگ‌ها
└── README.md
```
## 🔧 تنظیمات امنیتی پیاده‌سازی شده

۱. پنهان‌سازی اطلاعات سرور
 - server_tokens off;
۲. هدرهای امنیتی
 - add_header X-Frame-Options "SAMEORIGIN";
 - add_header X-XSS-Protection "1; mode=block";
 - add_header X-Content-Type-Options "nosniff";
 - add_header Referrer-Policy "no-referrer-when-downgrade";
 - add_header Content-Security-Policy "default-src 'self'";

۳. محدودیت دسترسی
## جلوگیری از لیست شدن دایرکتوری‌ها
autoindex off;

## مسدودسازی فایل‌های مخفی و حساس
location ~ /\. {
    deny all;
    access_log off;
    log_not_found off;
}

location ~* \.(env|log|sh|sql|conf|key|yml)$ {
    deny all;
    access_log off;
    log_not_found off;
}



