Các lớp permission có sẵn trong DRF

- **AllowAny**: cho phép truy cập không giới hạn
- **IsAuthenticated**: Chỉ cho phép người dùng đã đăng nhập truy cập vào
- **IsAuthenticatedOrReadOnly**: cho phép người dùng chưa đăng nhập chỉ được phép (READ) người dùng đã đăng nhập thì được phép (WRITE)

Cách sử dụng permission trong DRF
- **Cấu hình toàn cục**: trong file `setting.py` cấu hình bằng `DEFAULT_PERMISSION_CLASSES` 

```python

REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ]
}

```

- Cấu hình riêng cho từng view hoặc viewset: sử dụng thuộc tính `permission_class` trong class view hoặc viewset

```python
from rest_framework.permissions import IsAuthenticated
from rest_framework.views import APIView
from rest_framework.response import Response

class ExampleView(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request, format=None):
        content = {'status': 'request was permitted'}
        return Response(content)

```

- cấu hình cho function-base view: dùng decorator `@permission_classes` 

```python
from rest_framework.decorators import api_view, permission_classes
from rest_framework.permissions import IsAuthenticated
from rest_framework.response import Response

@api_view(['GET'])
@permission_classes([IsAuthenticated])
def example_view(request, format=None):
    content = {'status': 'request was permitted'}
    return Response(content)

```

Lưu ý: khi thiết lập `permission_class` trong view, nó sẽ ghi đè cấu hình mặc định trong `setting.py` 

**Custom permission** -> `BasePermission`

- kế thừa class `BasePermission` 
- override các phương thức `has_permission(self, request, view)` `has_object_permission(self, request, view, obj)` 

```python
from rest_framework.permissions import BasePermission

class IsOwnerOrReadOnly(BasePermission):
    """
    Cho phép người dùng chỉ sửa đối tượng nếu họ là chủ sở hữu,
    còn các phương thức đọc thì cho phép tất cả.
    """

    def has_permission(self, request, view):
        # Cho phép tất cả người dùng thực hiện các phương thức GET, HEAD, OPTIONS (đọc)
        if request.method in ('GET', 'HEAD', 'OPTIONS'):
            return True
        # Các phương thức khác yêu cầu đăng nhập
        return request.user and request.user.is_authenticated

    def has_object_permission(self, request, view, obj):
        # Cho phép đọc cho tất cả
        if request.method in ('GET', 'HEAD', 'OPTIONS'):
            return True
        # Chỉ cho phép chỉnh sửa nếu là chủ sở hữu của đối tượng
        return obj.owner == request.user

```

- sử dụng custom permission

```python
from rest_framework.views import APIView

class MyView(APIView):
    permission_classes = [IsOwnerOrReadOnly]

    # các phương thức get, post, put, delete...

```

