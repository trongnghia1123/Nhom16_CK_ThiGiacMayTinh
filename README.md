# NHẬN DIỆN VÀ DỰ ĐOÁN GƯƠNG MẶT ĐEO KHẨU TRANG BẰNG THỊ GIÁC MÁY TÍNH

- Nguyễn Trọng Nghĩa – 21031271
- Trương Xuân Hùng – 21090141

Đồ án tập trung phát triển và đánh giá hiệu suất của hai mô hình học sâu trong bài toán nhận diện và khôi phục gương mặt đeo khẩu trang, một ứng dụng quan trọng của thị giác máy tính. Nhóm sử dụng hai mô hình cho bài toán này là: **YOLO** được sử dụng để phát hiện nhanh và chính xác các vùng gương mặt, xác định trạng thái đeo khẩu trang và **U-Net** được áp dụng để tái tạo chi tiết và chân thực các đặc điểm gương mặt bị che khuất.

## Mô tả
- `Code/YOLO`: code YOLO
- `Code/U-Net`: code U-Net
- `Slide_Nhom16_CK.pptx`: Slide báo cáo 
- `Report_Nhom16_CK.docx`: Report báo cáo
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

