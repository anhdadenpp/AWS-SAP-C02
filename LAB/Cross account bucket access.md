# Follow link : https://docs.aws.amazon.com/res/latest/ug/S3-buckets-cross-account-access.html
## Bước 1: Tạo IAM Role trong Account A (tài khoản RES)
### 1. Đăng nhập vào AWS Management Console của Account A
### 2. Tại IAM Console tìm và chọn Policies
### 3. Tạo Policy 
- Chọn "Create policy"
- Chọn tab "JSON"
- Dán đoạn JSON policy sau (thay <BUCKET-NAME> bằng tên S3 bucket trong Account B)
   ```sh
  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:PutObject",
                "s3:ListBucket",
                "s3:DeleteObject",
                "s3:AbortMultipartUpload"
            ],
            "Resource": [
                "arn:aws:s3:::<BUCKET-NAME>",
                "arn:aws:s3:::<BUCKET-NAME>/*"
            ]
        }
    ]
}
- Chọn "Next"
- Đặt tên cho policy (ví dụ: "S3AccessPolicy")
- (optional) Thêm mô tả
- Chọn "Create policy"
### 4.Tạo Role 
- Chọn "Roles" trong menu bên trái
- Chọn "Create role"
- Chọn "Custom trust policy" làm loại trusted entity
- Dán đoạn JSON policy sau (thay <ACCOUNT_ID> bằng ID của Account A, <ENVIRONMENT_NAME> bằng tên môi trường RES, và <REGION> bằng region AWS của RES)
```sh
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::<ACCOUNT_ID>:role/<ENVIRONMENT_NAME>-custom-credential-broker-lambda-role-<REGION>"
            },
            "Action": "sts:AssumeRole"
        }
    ]
}
```
- Chọn "Next"
- Chọn policy bạn vừa tạo ("S3AccessPolicy")
- Chọn "Next"
- Đặt tên cho role (ví dụ: "S3AccessRole")
- Trong phần "Add Tag", thêm key là res:Resource và value là s3-bucket-iam-role
- Chọn "Create role"
  ### 5.Sử dụng IAM Role trong RES
  - Copy ARN của IAM role vừa tạo.
  - Đăng nhập vào RES console.
  - Chọn "S3 Bucket" trong menu bên trái.
  - Chọn "Add Bucket" và điền thông tin bucket S3 từ Account B.
  - Mở "Advanced settings - optional" và điền ARN của IAM role vào ô "IAM role ARN".
  - Chọn "Add Bucket".
  ## Bước 2: Sửa đổi Bucket Policy trong Account B
  - Đăng nhập vào AWS Management Console của Account B.
  - Mở S3 Console:
  - Tìm và chọn "S3" trong danh sách các dịch vụ.
  - Sửa Bucket Policy:
  - Chọn bucket bạn muốn cấp quyền truy cập.
  - Chọn tab "Permissions" và chọn "Bucket Policy".
  - Thêm policy sau (thay <AccountA_ID> bằng ID của Account A và <BUCKET-NAME> bằng tên bucket S3)
    ```sh
    {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::<AccountA_ID>:role/S3AccessRole"
            },
            "Action": [
                "s3:GetObject",
                "s3:PutObject",
                "s3:ListBucket",
                "s3:DeleteObject",
                "s3:AbortMultipartUpload"
            ],
            "Resource": [
                "arn:aws:s3:::<BUCKET-NAME>",
                "arn:aws:s3:::<BUCKET-NAME>/*"
            ]
        }
    ]
}
- Chọn "Save"
  ### Lưu ý quan trọng
- Thay thế các giá trị giữ chỗ: Đảm bảo bạn đã thay thế tất cả các giá trị như <BUCKET-NAME>, <ACCOUNT_ID>, <ENVIRONMENT_NAME>, <REGION>, và <AccountA_ID> bằng thông tin thực tế của bạn.
- Kiểm tra kỹ quyền: Xác minh rằng các quyền được cấp là đủ cho nhu cầu của bạn, nhưng không cấp quyền thừa để đảm bảo bảo mật.
- Tuân thủ nguyên tắc bảo mật: Luôn tuân thủ các nguyên tắc bảo mật của AWS khi cấp quyền truy cập giữa các tài khoản.
