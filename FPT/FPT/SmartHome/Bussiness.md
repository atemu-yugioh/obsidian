---
Status: Done
Start Date: 2025-04-01
End Date: 2025-04-30
---
Thực hiện gửi thông báo cho người dùng khi thiết bị IOT phát hiện các thay đổi

Danh sách các thiết bị IOT được thực hiện gửi notification

- PRESENSCE_SENSOR
- DOOR_SENSOR
- MOTION_SENSOR
- SMOKE_SENSOR
- GATE

Danh sách các service
- Iot message handler
	thực hiện consume message và push notification đến (opensearch + notification)
- cms: thực hiện config cho loại thiết bị (flfCategoryId) đó có gửi notification hay  không
- api-app: thực hiện cho phép người dùng bật/tắt notification đối với 1 thiết bị

Flow

- consume message và tiến hành thực hiện check + gửi notification
- những thông tin có được từ message
	- rogoId: id của thiết bị (profileDeviceId)
	- attrCode: cho biết thiết bị đó thực hiện hành động nào
	- value: thường là 0/1 cho biết trạng thái
	- elementId: nếu là element thì có thêm elementId
- check
	- profileDevice của thiết bị có tồn tại không
	- nếu là devTypeCode = 19 và rogoDevSubTypeCode = 30 (MOTOR_CONTROLLER) thì không gửi notify
	- nếu profileDevice tồn tại thì check người dùng của thiết bị đó có bật notification cho thiết bị đó không
	- check thiết bị đó có đang được cấu hình (cms) để gửi notification không
- gửi notification
	- gửi lên opensearch để lưu lại thông tin để người dùng lấy danh sách thông báo về xem
	- sau đó gửi notification đến người dùng
- riêng thiết bị là SMOKE_SENSOR auto gửi notification
		