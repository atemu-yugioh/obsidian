#fli #b2c


Refactor (PIC a Thieng, Hoa support):   
  - Cover Business [[FLI business core]] Interface:  
    + Action  --> Interface
    + Attribute  --> business core
    + Targets:  
      - Basic Device Information (include Device authorization)  
	      - --> view camera authorization
	      - --> device authorization
      - Device Package ----------------------------------------------- !!! HIGH Priority  
	      - --> camera package 
	      - --> iot-device package (hiện tại iot-device chưa có package, nhưng nếu có thì sao, quản lý ra sao, ở đâu, quản lý chung với camera package được không, nếu không thì bất cập là gì)
	      - --> review and combine
      - Device Features:  (làm rõ hai khái niệm hardware và firmware)
        + Hardware  
        + Firmware  
      - Device Settings (Stateful feature)  
  - Implement Interface:  
    + Camera  
    + IoT Device  
  - Packaging Service with Interface (Customer, Camera Management)  
  - Expose Events from actions with Interface:  (tham khảo even-driven, even-bus, CQRS)
    + Camera: Customer, Camera Management  
    + Smarthome: IoT Devices  
  - Implement New Services:  (đề xuất kiến trúc hexagonal cho new service)
    + Device Authorization  
    + CMS for Device Features  
  - Sync Events to New Services:  (tham khảo even-driven, even-bus)
    + Implement Adapter for Event Interface  
    + Expose APIs for functional


- research tech
	- hexagonal architecture
	- event driven, even bus
	- CQRS
- todo
	- review camera package, những thứ liên quan đến camera package
		- entity, model
		- business
	- những api nào đang liên quan đến camera package
		- những api có đang phụ thuộc service nào không
			- nếu có thì ở đâu --> expose event
	- các action mà camera package đang có (thêm, xóa, sửa ...) (business core) (1)
	- các thông tin thuộc tính (business core) (2)
		- (1+2) ==> Interface (CQS or CQRS)
		- ==> build service để migration logic theo interface
		- 