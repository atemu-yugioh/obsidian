
Đăng ký 1 `**gis**` package có 

```python

apps > apis > utils.py

class APIAccessPermission(permissions.BasePermission)

 - class init nhận vào 1 stack (feature like: `rest_api_camera_info`)
 - kiểm tra `**gis**` có được gửi lên hay không thông qua 'HTTP_GIS' từ request.META
 - lấy thông tin registration và danh sách feature mà `**gis**` sở hữu
 - nếu `type` là 'web' thì check 'HTTP_HOST' có trùng với 'package' không
 - nếu `type` khác check 'HTTP_PACKAGE' có trùng với 'package' không
 - check stack feature hiện tại có nằm trong list_feature của `**gis**` không
```

**Cấu trúc `Registration` và `Feature`** 

```python
class Feature(models.Model):

    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)

    name = models.CharField(max_length=100, unique=True)

    type = models.CharField(max_length=100)

    brief = models.TextField(blank=True, null=True)

    created_at = models.DateTimeField(auto_now_add=True)

    created_by = models.CharField(max_length=150, null=True)

    modified_at = models.DateTimeField(auto_now=True)

  

    def __str__(self):

        return u'[{}] {}'.format(self.type, self.name)
```

```python
class Registration(models.Model):

    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)

    app_package = models.CharField(max_length=200, verbose_name=_('Package'))

    app_id = models.CharField(unique=True, max_length=50, null=True, verbose_name=_('ID'))

    app_type = models.CharField(max_length=200, verbose_name=_('Type'), choices=APP_TYPE_CHOICES)

    server = models.BooleanField(default=1, help_text=_(u'Provide server account to this user'), verbose_name=_('Server status'))

    features = models.ManyToManyField(Feature, related_name='registration_features')

    status = models.BooleanField(default=1, choices=STATUS_CHOICES)

    created_by = models.CharField(max_length=150, null=True)

    created_at = models.DateTimeField(auto_now_add=True)

    note = models.CharField(max_length=100, blank=True, null=True)

  

    def __str__(self):

        return u'{}'.format(self.app_package)

  

    def save(self, *args, **kwargs):

        if not self.app_id:

            self.app_id = uuid.uuid4().hex

        super(Registration, self).save(*args, **kwargs)
```

