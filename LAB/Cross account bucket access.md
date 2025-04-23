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
  ```
