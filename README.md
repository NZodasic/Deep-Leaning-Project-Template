# Deep-Leaning-Project-Template

Mẫu dự án Deep Learning này cung cấp khung làm việc đồng nhất cho việc xây dựng các dự án Deep Learning trong môi trường TensorFlow V2. Mẫu chia một dự án Deep Learning thành các phần chính sau:

- **Preprocessor**: Thực hiện xử lý trước dữ liệu (tùy chọn).
- **Dataloader**: Tạo bộ tải dữ liệu, thường sử dụng `tf.data.Dataset` trong TensorFlow V2.
- **Model**: Xây dựng một mô hình mạng não sâu, kết quả là một đối tượng `tf.keras.Model`.
- **Trainer**: Xác định chi tiết quy trình huấn luyện, bao gồm việc sử dụng dữ liệu và mô hình.
- **Config**: Cung cấp các tham số siêu, tham số cài đặt để truyền qua các phần khác nhau trong dự án.

## Cài đặt và sử dụng

Khuyên dùng Git submodule để thêm mẫu này như một thư mục con trong dự án. Lưu ý rằng các thay đổi trong submodule chỉ có thể được commit vào repository của submodule.

Lệnh thêm submodule:
```shell
git submodule add git@github.com:NZodasic/Deep-Leaning-Project-Template.git templates
```

Sau khi thực thi, tệp tin `.gitmodules` và thư mục `templates` sẽ được tạo. Khi commit, hãy đảm bảo commit cả hai.

Nhập mẫu trong Python:
```python
from templates import *
```

## Các lớp mẫu

### ConfigTemplate

Lớp ConfigTemplate được sử dụng để truyền tham số qua các lớp khác trong dự án. Các tham số được truyền qua phương thức `__init__`.

```python
class XXX_TrainerConfig(ConfigTemplate):
    def __init__(learning_rate, epoch):
        self.LR = learning_rate
        self.EPOCH = epoch
```

Trong các lớp khác, tham số có thể truy cập bằng `self.config.XXX`.

### DataLoaderTemplate và PreprocessorTemplate

Cả hai lớp này đều liên quan đến xử lý dữ liệu. Tuy nhiên, DataLoaderTemplate tập trung vào việc tạo một đối tượng `tf.data.Dataset`.

Phương thức load() phải được ghi đè để xác định quy trình tải dữ liệu. Kết quả phải được lưu vào `self.dataset`.

```python
class XXX_DataLoader(DataLoaderTemplate):
    def load():
        ...
        self.dataset = tf.data.Dataset.from_tensor_slice((image, label))
```

Dữ liệu đã tải có thể truy xuất qua phương thức `get_dataset()`.

### ModelTemplate

Lớp ModelTemplate được dùng để định các mô hình TensorFlow, thường sử dụng API của Keras để tạo mô hình `tf.keras.Model`. Mô hình sau khi tạo phải được lưu trong `self.model`.

### TrainerTemplate

TrainerTemplate chịu trách nhiệm xây dựng quy trình huấn luyện. Trong lúc khởi tạo, Trainer phải nhận được mô hình và bộ dữ liệu.

Trainer xác định cách mô hình sử dụng dữ liệu để huấn luyện.

### Ví dụ tham khảo
-  https://github.com/acherstyx/Deep-Leaning-Project-Template











