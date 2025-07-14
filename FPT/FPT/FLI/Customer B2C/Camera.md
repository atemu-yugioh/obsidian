

1. property
- object: ???
- family: ???
- serial: serial của camera
- id: string
- name: string
- product_code: string
- alerts: relation đến customer để làm gì ???  -> Customer interface
- status: int
	- -1: Unknown
	- 0: Offline
	- 1: Online
- place: relation đến Place để lấy thông tin place ->  Place interface
- owner: relation đến Customer để lấy thông tin owner -> Customer interface
- activate_at: Date
- is_wifi: boolean
- recorder: dùng để làm gì -> Recorder interface
- cmr_type: enum
- is_smart: boolean
- room: relation đến Room để lấy thông tin room
- business_type: enum
- camera_image
- camera_type
- is_not_require_package
- CAMERA_MODEL: enum
- has_wifi
- camera_model_name
- CameraSettings
- CameraFeature
- CameraPackage`
- CameraSharerRequest
- CameraSharer
- CameraPackageTemp
- CameraTopic
- CameraConstruction`
- 

1. action
- get_serial_by_prod_code
	- input: product_code
	- serial
- camera_type_from_product_code
	- input: product_code
	- cmr_type
- get_fml_permission
	- input: user_id
	- CustomerACL: int
- 
