---
title : "Đóng gói Docker Image"
date : "2024-05-15"
weight : 1
chapter : false
pre : " <b> 5.7.1. </b> "
---

1. Viết `Dockerfile` dựa trên `debian:bookworm-slim`, cài `default-mysql-client`, `awscli`, `gzip`.
2. Viết script `backup_db.sh` đọc cấu hình qua biến môi trường (`DB_HOST`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`, `S3_BUCKET`), thực thi `mysqldump` (không dùng `--set-gtid-purged` vì MariaDB client không hỗ trợ), nén và đẩy lên S3.

   ![Nội dung Dockerfile và backup_db.sh](/images/5/5.7.1/01-dockerfile-backup-sh.png?classes=border,shadow)

   ![Tiến trình thực thi lệnh docker build thành công](/images/5/5.7.1/02-docker-build.png?classes=border,shadow)

   ![Docker Image cục bộ sẵn sàng đóng gói](/images/5/5.7.1/03-docker-images.png?classes=border,shadow)
