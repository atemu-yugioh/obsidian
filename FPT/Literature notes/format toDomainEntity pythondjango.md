---
aliases:
  - format toDomainEntity python/django
---
Python **không có `plainToClass()` built-in**, nhưng ta có thể **tạo một phiên bản giống vậy**, rất ngắn gọn.

✅ Giải pháp: Viết hàm `plain_to_entity()` giống `plainToClass`

Dưới đây là cách bạn tạo một helper để convert `DjangoModel` hoặc `dict` thành domain entity:

Ví dụ dùng với `@dataclass`:

```python
from dataclasses import is_dataclass, fields

def plain_to_entity(entity_class, plain_data):
    if not is_dataclass(entity_class):
        raise ValueError("Entity class must be a dataclass")

    data = {}

    for f in fields(entity_class):
        if isinstance(plain_data, dict):
            value = plain_data.get(f.name)
        else:  # Django model object
            value = getattr(plain_data, f.name, None)

        data[f.name] = value

    return entity_class(**data)

```

✅ Sử dụng:

```python
camera_entity = plain_to_entity(CameraEntity, camera_package_django)
```

🧩 Option nâng cao: `pydantic` như `class-transformer`

Nếu bạn dùng `pydantic`, thì có sẵn behavior gần giống `plainToClass()`:

```python
from pydantic import BaseModel

class CameraEntity(BaseModel):
    id: str
    subscription: int
    camera_id: str
    ...

camera_entity = CameraEntity.model_validate(camera_package_django.__dict__)

```

✅ `model_validate()` tự bỏ field thừa, tự ép kiểu → rất giống TypeScript `plainToClass`.