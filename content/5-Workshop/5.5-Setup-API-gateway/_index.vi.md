---
title : "VPC Endpoint Policies"
date: 2025-09-09
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

**1. Vào API gateway**
- Nhấp vào create an api
![alt text](image.png)
- Chọn build trong Rest api
![alt text](image-1.png)
- Nhập tên 
![alt text](image-2.png)
- Chọn policy security
![alt text](image-3.png)
- Nhấp chuột vào create API
**2. Tạo Resource**
- Nhấp vào create resource
![alt text](image-4.png)
- Đặt tên resource và tick vào CORS
![alt text](image-5.png)
- Nhấp chuột vào nút create resource
**3. Create method**
- Nhấp chuột vào create method
![alt text](image-6.png)
- Chọn phương thức post và bật Lambda proxy integration
![alt text](image-7.png)
- Thêm ARN
![alt text](image-8.png)
- Nhấp chuột vào create method
**4.deploy API**
-  Nhấp chuột vào deploy API
![alt text](image-9.png)
- Chọn new stage và đặt tên cho stage
![alt text](image-10.png)
- Nhấp chuột vào nút deploy
**5. Test**
- Sau khi tạo stage xong bạn sẽ có được Invoke URL
  ![alt text](image-11.png)
- Nhập invoke url để test trên postman với cú pháp invoke url/Tên resource, chọn phương thức post
  ![alt text](image-12.png)
- Nhập
  
  {
    "message": "amazon bedrock là gì?, nói ngắn gọn không quá 3 dòng"
  }
 
- Sau khi Nhấp chuột vào send
![alt text](image-13.png)
- Vậy là bạn đã thành công