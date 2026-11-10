# Báo cáo cá nhân — Ngày 2 Object Detection


## 1. Thông tin học viên

- Họ tên: Hoàng Quốc Chung
- MSSV: 2A202604039
- Email: 26ai.chunghq2@vinuni.edu.vn
- Lớp: L2B
- Link repo bài làm: https://github.com/qchung2124/K5-L2B-DAY02-HoangQuocChung-2A202604039-ObjectDetection
- Link Colab đã chạy: https://colab.research.google.com/drive/1d7h65cpp0cO7tMh9mkV2CME2wxJminwl#scrollTo=6Aq6jjs2elfl

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](./GUIDELINE_MINI.md). 
## 3. Annotation và self-QC

- Số file nhãn train: 50 file (`drive_001.txt` đến `drive_050.txt`)
- Kết quả checker và lỗi đã xử lý: Tự kiểm tra bằng script Self-QC (CP3) đạt 50/50 file hợp lệ. Xử lý các lỗi tọa độ out-of-bounds `[0, 1]` và định dạng ID class.
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: `drive_001.jpg`, `drive_005.jpg`, `drive_010.jpg`, `drive_015.jpg`, `drive_020.jpg`, `drive_025.jpg`, `drive_030.jpg`, `drive_035.jpg`, `drive_040.jpg`, `drive_045.jpg`.
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: Phát hiện một số box bao quanh xe car ở xa bị rộng viền và nhầm lẫn giữa `van` với `car`. Đã điều chỉnh lại tọa độ box ôm sát thân xe và sửa ID class về đúng schema.
- Commit khóa nhãn ban đầu: ba59706

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP | 520 | |
| FP | 102 | |
| FN | 133 | |
| Precision | 0.836 | |
| Recall | 0.7963 | |
| F1 | 0.8157 | |
| mean_iou_of_matches | 1.0 | |
| passed | true | |

Dẫn tới [outputs/annotation_evaluation.json](./outputs/annotation_evaluation.json) trong repo.
Không có rewwork.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: Google Colab (Tesla T4 GPU, 14.9 GiB VRAM), Ultralytics 8.4.208, PyTorch 2.14.1+cu130, Python 3.13.16.
- Các tham số thay đổi so với notebook nếu có và lý do: Giữ nguyên các tham số mặc định của notebook (yolo26n.pt, 30 epochs, batch=16, imgsz=640, device=0) để đảm bảo tính nhất quán của thực nghiệm.
- Đường dẫn best checkpoint trong phiên chạy: /content/Day2-Lab/outputs/yolo26_runs/vehicle_annotation/weights/best.pt

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | 0.284 |
| Recall | 0.303 |
| mAP50 | 0.296 |
| mAP50–95 | 0.213 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
    - Lớp có Recall thấp nhất: Lớp bus ($Recall = 0$).
    - drive_052.jpg.
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
    Cần kiểm tra độ chính xác định vị ranh giới (bounding box tightness & alignment) của các ô bao dự đoán xem có ôm khít vật thể hay không.
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
    - Lỗi liên quan guideline: Nhầm lẫn phân loại giữa bus / van / truck thành car.
    - Dữ kiện:
        - Quy định trong Guideline dựa vào kiểu dáng thùng xe và kích thước để phân biệt car với van/truck/bus. Tuy nhiên, các góc chụp camera từ trên cao làm tiêu biến độ nổi chiều cao của xe.
        - Tập train chỉ có 50 ảnh làm cho số lượng mẫu bus/van quá ít so với car, làm mô hình bị hiện tượng thiên vị (bias) nghiêng về lớp chiếm đại đa số mẫu (car).

4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
    - Lý do không dùng 10 ảnh eval để train: Tránh hiện tượng rò rỉ dữ liệu. Tập eval đóng vai trò là "đề thi độc lập" dùng để kiểm thử khả năng tổng quát hóa của mô hình trên dữ liệu mới chưa từng được học. Nếu đưa 10 ảnh này vào train, mô hình sẽ "học thuộc lòng" và cho chỉ số cao ảo nhưng mất khả năng dự đoán thực tế.
    - Vai trò Validation trong notebook: Dùng để đánh giá hiệu năng mô hình sau mỗi epoch, từ đó giúp tự động chọn ra trọng số tốt nhất (best.pt) trong quá trình huấn luyện.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| | | | |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
