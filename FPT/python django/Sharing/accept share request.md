**Input**

```json
{
    "id": "70c5bb0e11c743f5ad4eff1754d83b8b"
}
```

- kiểm tra request tồn tại
- kiểm tra status đã được update (status != pending)
- kiểm tra xem danh sách thiết bị được chia sẻ có còn khả dụng không
- thực hiện accept request share cho từng loại device (camera, iot, element)
