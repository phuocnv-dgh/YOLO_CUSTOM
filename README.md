# CountProducts
1. cai dat cuda tookit -> nvidia-smi tu dong nhan
2. cai dat cudnn
3. cai opencv dev: sudo apt install libopencv-dev
4. mkdir backup custom_data custom_weight


-----------------------------

Phần 2 – Chi tiết bước chỉnh sửa file config

Đại khái cách train mình đã có bài rất chi tiết rồi, các bạn có thể tìm lại tại đây. Mình chỉ đi sâu vào phần chỉnh sửa file yolov3-tiny.cfg vì nó khác đôi chút với chúng ta train YOLOv3 thông thường.

Các bạn tiến hành sửa file yolov3-tiny.cfg theo cách sau:

    Tìm đến dòng số 3, sửa batch=24 thay cho batch =64. Đây là số ảnh load vào RAM mỗi lần train.
    Tìm đến dòng số 4, sửa subdivisions=8
    Tìm đến dòng 127, chỉnh lại filters=(num_class + 5)*3 trong đó num_class là số lớp bạn cần train. Ví dụ train nhận mỗi súng thì num_class = 1 (thì filter sẽ là (1+5)*3=18), nếu train để nhận cả súng và dao thì num_class=2…
    Tìm đến dòng 135, sửa lại classes = num_class (num_class là số lớp đó).
    Sửa dòng 171 giống dòng 127 và dòng 177 giống dòng 135.

python3 custom_data/creating-train-and-test-txt-files.py

 Train: ./darknet/darknet detector train custom_data/labelled_data.data darknet/cfg/yolov3-tiny.cfg custom_weight/darknet53.conv.74
