---
title : "Docker Image Packaging"
date : "2024-05-15"
weight : 1
chapter : false
pre : " <b> 5.7.1. </b> "
---

1. Create `Dockerfile` based on `debian:bookworm-slim`, install `default-mysql-client`, `awscli`, `gzip`.
2. Create `backup_db.sh` reading runtime environment variables (`DB_HOST`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`, `S3_BUCKET`), executing `mysqldump`, compressing and streaming backup to S3.

   ![Dockerfile and backup_db.sh script contents](/images/5/5.7.1/01-dockerfile-backup-sh.png?classes=border,shadow)

   ![Successful local docker build execution](/images/5/5.7.1/02-docker-build.png?classes=border,shadow)

   ![Local docker images inventory ready for deployment](/images/5/5.7.1/03-docker-images.png?classes=border,shadow)
