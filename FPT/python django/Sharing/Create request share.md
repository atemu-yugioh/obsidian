
**Input**

```json
{
  "tagging_sharer": "share 1-n iot-device",
  "objects": [
    {
      "type": "iot-device",
      "device_id": null,
      "object_ids": [
        "40772ee4-d7db-4efc-b029-97f1a3fef568",
        "8e526efd-0c30-4a92-a84c-f3c03e61afaf"
      ]
    }
  ],
  "country_code": "+84",
  "phone_number": "0938810289",
  "interval": 0,
  "token": ""
}
```


- kiểm tra có chia sẻ cho chính nó không `_validate_not_self` 
- kiểm tra thằng được chia sẻ tồn tại trong hệ thống không `_validate_users_exist` 
- với objects cần kiểm tra thiết bị có thỏa mãn điều kiện được tiếp tục share hay không
	- kiểm tra quyền của thằng owner với mỗi object (device, element, camera ...) `_validate_objects_permissions`
	- kiểm tra object đã được chia sẻ cho thằng sharer trước đó chưa (gồm đã chia sẻ và đang có request chứa object đó)
	- kiểm tra dung lượng chia sẻ cho mỗi object `_validate_capacity` (`MAX_SHARER_ALLOW` và max_sharer_allow của gói đối với camera)
- tạo share request
- notification đến sharer (nếu có)



- api tạo lời mời chia sẻ
- api từ chối lời mời chia sẻ
- api gỡ chia sẻ 1 thiết bị cho 1 danh sách người dùng
- api gỡ chia sẻ 1 danh sách thiết bị cho 1 người dùng
- api đồng ý lời mời chia sẻ
- api thông tin sharing trên account (danh sách người dùng đã chia sẻ, danh sách thiết bị đã chia sẻ, danh sách các lời mời đang gửi)
- api thông tin được sharing cho account (danh sách lời mời, danh sách thiết bị được chia sẽ cho account)
- api thông tin sharing của 1 thiết bị (danh sách người dùng đã chia sẻ, danh sách lời mời đang chứa thiết bị này, thông tin chi tiết của thiết bị)
- api thông tin chi của 1 lời mời chia sẻ
- api thông tin danh sách thiết bị đã được chia sẻ cho 1 người dùng (số lượng nhà, phòng đã chia sẻ, danh sách thiết bị đã chia sẻ)
- api kiểm tra xem 1 danh sách thiết bị đã được chia sẻ cho 1 người dùng chưa (dung lượng tối đa được chia sẻ, số lượng đã chia sẻ, trạng thái chia sẻ đối với 1 người dùng)
- api thông tin danh danh sách người dùng đã chia sẻ trên 1 thiết bị (dung lượng tối đa được chia sẻ, danh sách người dùng đã được chia sẻ)
- api share gỡ chia sẻ 1 thiết bị
- api danh sách người dùng được đề xuất để chia sẻ thiết bị
- api danh sách thiết bị được đề xuất đề chia sẻ