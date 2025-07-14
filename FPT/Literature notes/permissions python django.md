
- tìm hiều permission trong django, tìm hiểu cú pháp hay được sử dụng trong source b2c
```python
@permission_classes((
	permissions.IsAuthenticated, 
	partial(APIAccessPermission, 'api_camera_motion_zone_update'),
))
```