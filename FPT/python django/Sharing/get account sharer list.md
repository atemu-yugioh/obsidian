**Output**

```python
{
    "result": true,
    "message": "Success",
    "code_status": 1200,
    "data": [
        {
            "shared_list": [], --> danh sách người dùng đã chia sẻ
            "request_list": [], --> danh sách lời mời đã gửi
            "shared_device_list": [] --> danh sách thiết bị đã chia sẻ
        }
    ],
    "data_error": [],
    "errors": []
}
```


- lấy danh sách request (request_list) của user
	- valid_request: lọc ra nhưng request có status == PENDING và chưa hết hạn
	- format request_list
- lấy danh sách shared object (danh sách thiết bị đã chia sẻ và danh sách người dùng đã chia sẻ)
	- lấy thông tin chi tiết của các thiết bị được chia sẻ
	- lấy danh sách người dùng được chia sẻ