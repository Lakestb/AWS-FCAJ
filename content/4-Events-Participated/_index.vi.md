---
title : "Các events đã tham gia"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

### Báo cáo Sự kiện – First Cloud Journey (FCAJ)

---

### 1. Thông tin sự kiện

* **Tên sự kiện**: First Cloud Journey – Cloud Computing, System Design & MLOps on AWS
* **Mục tiêu của sự kiện**:
  * Cung cấp bức tranh toàn diện và lộ trình thực tế cho sinh viên, kỹ sư phần mềm bắt đầu với nền tảng điện toán đám mây AWS.
  * Làm rõ kiến trúc thiết kế hệ thống từ cơ bản đến quy mô lớn (System Design).
  * Đi sâu vào các mô hình lưu trữ máy chủ (Hosting Spectrum).
  * Xây dựng quy trình Data Science & MLOps hoàn chỉnh từ thử nghiệm đến production trên hạ tầng Cloud.
* **Diễn giả**:
  * **Phuong Nguyen Huu**: Trình bày chủ đề *"The Very First Step into Cloud"*.
  * **Vu The Huy**: Data Engineer, trình bày chủ đề *"Data Science & MLOps on AWS"*.
  * **Quang Pham**: DevOps Engineer, trình bày chủ đề *"Right Server, Right Job – Comparing Hosting Types and Server Options"*.
  * **Lê Thành Dũng (ltdungg)**: Giảng viên / Tác giả bộ tài liệu *"System Design cho người mới bắt đầu"*.

---

### 2. Những nội dung nổi bật

#### 2.1. The Very First Step into Cloud (Nhập môn Điện toán đám mây)
* **Khái niệm Cloud & Lợi ích kinh tế**: 
  * So sánh On-Premises với Cloud.
  * Chuyển dịch từ chi phí đầu tư hạ tầng cố định (CapEx) sang chi phí vận hành linh hoạt (OpEx).
  * Tận dụng lợi thế quy mô (Economies of Scale) và khả năng mở rộng quy mô toàn cầu trong vài phút.
* **Mô hình dịch vụ & Trách nhiệm chia sẻ**: 
  * Phân định rõ IaaS, PaaS, SaaS.
  * Mô hình Shared Responsibility Model (Bảo mật *trong* Cloud của khách hàng vs. Bảo mật *của* Cloud do AWS đảm nhận).
* **Hạ tầng toàn cầu AWS**: 
  * Cấu trúc gồm Regions, Availability Zones (AZs) và Edge Locations.
  * Các phương thức tương tác quản trị qua AWS Console, AWS CLI và AWS SDKs.

#### 2.2. System Design cho người mới bắt đầu (Thiết kế hệ thống)
* **Từ một Server đến Hệ thống mở rộng**: Phân tích ba điểm nghẽn / failure đầu tiên khi chạy một server duy nhất cho ứng dụng chia sẻ ảnh.
* **Phân định kiến trúc**: 
  * High-Level Design (HLD) vs. Low-Level Design (LLD).
  * Thiết lập Functional và Non-functional Requirements (NFRs).
  * Monolith vs. Microservices; Vertical Scaling (mở rộng dọc) vs. Horizontal Scaling (mở rộng ngang).
* **Hạ tầng cốt lõi và Tối ưu dữ liệu**: 
  * Cơ chế hoạt động của DNS/HTTPS, Load Balancer (Health checks, Reverse Proxy, thuật toán điều phối), máy chủ Stateful vs. Stateless.
  * Chiến lược Data Modeling, SQL vs. NoSQL, Database Indexing, Caching (TTL, Stampede), Database Replication và Sharding.

#### 2.3. Right Server, Right Job: So sánh các loại Hosting & Server
* **The Hosting Spectrum**: Phân tích 5 mô hình lưu trữ: Shared Hosting, VPS, VDS, Dedicated Server và On-Premises (tương ứng với các dịch vụ AWS như Amplify/App Runner, EC2 T-series, EC2 Compute-Optimized, EC2 Dedicated Host, AWS Outposts).
* **Bản chất kiến trúc & Tránh lỗi thường gặp**:
  * Shared Hosting dùng cgroups/namespaces; VPS chia sẻ tài nguyên CPU qua Type-1 hypervisor dẫn đến tình trạng CPU Steal.
  * VDS sử dụng CPU pinning kết hợp NUMA-aligned RAM để tránh mất hơn 50% hiệu năng do Cross-Node Memory Access.
  * **Kiến trúc AWS Nitro System**: Offload toàn bộ I/O, mạng và lưu trữ sang phần cứng chuyên dụng, trả lại gần như 100% tài nguyên CPU/RAM cho máy ảo.
* **Case Study thực tế**: Kiến trúc Hybrid Cloud của athenahealth kết hợp giữa Datacenter on-premise, AWS Outposts và AWS Local Zones để hiện đại hóa hệ thống mà vẫn duy trì độ khả dụng cao.

#### 2.4. Data Science & MLOps on AWS
* **Bức tranh tổng quan (DE vs. DS vs. DA)**: Phân biệt rõ ràng vai trò giữa Data Engineer ("Người làm đường"), Data Scientist ("Người dự đoán") và Data Analyst ("Người kể chuyện").
* **Thực tế công việc của Data Scientist**: 70% thời gian dành cho bài toán nghiệp vụ, EDA và Feature Engineering; chỉ 20% cho huấn luyện/đánh giá mô hình và 10% cho triển khai.
* **Case Study Churn Prediction & Quy trình End-to-End**:
  * **Data Lake & Data Catalog**: Tích hợp AWS S3, AWS Glue và AWS Athena/EMR.
  * **Quản lý Features**: AWS SageMaker Feature Store đồng bộ hóa online/offline, chống Data Leakage.
  * **Model Serving & MLOps**: Triển khai Real-time Inference qua SageMaker Endpoints (REST API, Auto-scaling) và Batch Transform cho dữ liệu lớn; tự động hóa quy trình với SageMaker Pipelines và giám sát Data Drift/Model Drift qua SageMaker Model Monitor.
  * **XAI & Bias Detection**: SageMaker Clarify giúp giải thích dự đoán và phát hiện thiên vị dữ liệu.

---

### 3. Kiến thức tiếp thu

* **Điện toán đám mây & Hạ tầng (Cloud & Infrastructure)**:
  * Nắm vững mô hình Shared Responsibility Model giúp xác định chính xác trách nhiệm cấu hình bảo mật dữ liệu, mã nguồn và hệ điều hành.
  * Hiểu sâu về AWS Nitro System và kiến trúc mạng On-Premises / Hybrid với AWS Outposts.
* **Thiết kế hệ thống (System Design)**:
  * Nắm rõ các câu hỏi mấu chốt trước khi thiết kế: Scale, Read/Write ratio, Durability, Latency và Cost.
  * Hệ thống Stateless cho phép mở rộng ngang (Horizontal Scaling) mượt mà kết hợp cùng Load Balancer và Cache nhiều tầng.
  * Nắm vững kỹ thuật xử lý dữ liệu ở tầng cơ sở dữ liệu: Replication (lag, failover), Sharding (shard key, consistent hashing) và Indexing.
* **Trí tuệ nhân tạo & MLOps (AI & Machine Learning)**:
  * Mô hình chạy tốt trên Jupyter Notebook chưa đủ để ra sản phẩm thực tế; cần tư duy MLOps để giải quyết bài toán tải cao, đồng bộ feature và tự động retrain khi xảy ra data drift.
  * Việc đóng gói mô hình thành REST API (FastAPI) hoặc giao diện web tương tác (Streamlit/Gradio) giúp thể hiện trọn vẹn tư duy End-to-End của kỹ sư dữ liệu.

---

### 4. Cảm nhận sau sự kiện

* Các bài học trong chuỗi chuyên đề đã mang lại góc nhìn thực tế và có tính hệ thống cao, kết nối trực tiếp giữa lý thuyết hàn lâm và kiến trúc triển khai thực tế tại doanh nghiệp.
* Nội dung so sánh sâu về hạ tầng phần cứng máy chủ (từ CPU Steal của VPS đến NUMA memory của VDS và Nitro System) đã giải tỏa được nhiều ngộ nhận phổ biến khi lựa chọn cấu hình máy chủ. 
* Đồng thời, bức tranh toàn diện về MLOps trên AWS SageMaker và chuỗi bài giảng System Design từng bước đã định hình rất rõ phương pháp tư duy kiến trúc khi xây dựng một hệ thống phần mềm có khả năng chịu tải hàng triệu người dùng.

---

### 5. Bài học rút ra

1. **Lựa chọn máy chủ theo tải thực tế**: Không nên mặc định chọn giải pháp đắt tiền ngay từ đầu; hãy đánh giá theo 4 trục: **Chi phí, Độ ổn định/dự đoán được, Tuân thủ quy định và Quy mô** (Cost, Predictability, Compliance, Scale).
2. **Tránh bẫy cục bộ trong Machine Learning**: Đừng chỉ dừng lại ở các bài toán Kaggle hay file `.ipynb` – cần rèn luyện tư duy đưa mô hình ra môi trường thực tế (REST API, Monitoring, Feature Store, CI/CD Pipeline).
3. **Thiết kế hệ thống có chủ đích**: Mọi thành phần kiến trúc (Load Balancer, Caching, Read Replica, Sharding) chỉ nên đưa vào khi hệ thống gặp điểm nghẽn thực sự.
4. **Bảo mật là trách nhiệm song hành**: Luôn chủ động mã hóa dữ liệu và kiểm soát phân quyền (IAM) thay vì phó mặc hoàn toàn cho nhà cung cấp đám mây.
