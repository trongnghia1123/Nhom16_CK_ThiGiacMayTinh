# Nhóm 16 - NHẬN DIỆN VÀ DỰ ĐOÁN GƯƠNG MẶT ĐEO KHẨU TRANG BẰNG THỊ GIÁC MÁY TÍNH

- Trương Xuân Hùng – 21090141
- Nguyễn Trọng Nghĩa – 21031271

## Mô tả
Code/YOLO chứa code YOLO
Code/U-Net chứa code U-Net

## 1. Dữ liệu
Bộ dữ liệu được sử dụng là "Face Mask Detection Dataset", được thu thập từ Kaggle (https://www.kaggle.com/datasets/ashishjangra27/face-mask-12k-images-dataset). Nhóm chỉ sử dụng dữ liệu ảnh gương mặt không đeo khẩu trang và dùng một prọect có sẵn trên github ([MaskTheFace](https://github.com/aqeelanwar/MaskTheFace?ref=strv.ghost.io)) gắn khẩu trang tạo ra dữ liệu mới với gương mặt được đeo khẩu trang.

## 2. Trainning
### YOLO
Mô hình được huấn luyện với bộ dữ liệu 8549 ảnh trong đó được chia thành ba phần với các tỷ lệ: 70% train, 15% test, 15% validation. Mô hình YOLOv8n huấn luyện với khoảng 3tr tham số, 72 layer. Tham số huấn luyện như sau:

| Thông số | Giá trị |
|:-------:|:-------:|
| Epoch | 100 |
| Batch size | 32 |
| Learning rate | 0.01 - 0.001 |
| Early stopping | 20 |
| Optimizer | AdamW |

### U-Net
Mô hình được huấn luyện với bộ dữ liệu 4042 ảnh trong đó được chia thành ba phần với các tỷ lệ: 70% train, 20% test, 10% validation. Mô hình được huấn luyện bằng GPU trên Kaggle. 
Tham số huấn luyện như sau:

| Thông số | Giá trị |
|:-------:|:-------:|
| Epoch | 100 |
| Batch size | 8 |
| Learning rate | 0.001 |
| Early stopping | 10 |
| Optimizer | Adam |

## 3. Inference
### YOLO
Mô hình YOLOv8 được huấn luyện và đánh giá cho bài toán nhận diện gương mặt và khẩu trang đạt hiệu suất tốt trên cả tập validation và test. Hình ảnh dự đoán cũng đạt được kết quả tốt.

### U-Net
Mặc dù các chỉ số đánh giá định lượng như SSIM, PSNR, LPIPS và MAE cho thấy mô hình đạt kết quả khá tốt, nhưng các đặc điểm khuôn mặt quan trọng như mũi và miệng – vốn đóng vai trò then chốt trong việc nhận diện khuôn mặt – thường không được tái hiện rõ nét hoặc bị mờ nhòe, làm giảm tính chân thực và tự nhiên của ảnh đầu ra.

