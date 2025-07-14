
```python
MIDDLEWARE = [

    # ... other middleware

    'your_app.utils.errors.ErrorHandlingMiddleware',

]
# MIDDLEWARE có tác dụng gì, dùng ở đâu, khi nào được dùng
```

```python
REST_FRAMEWORK = {
    'EXCEPTION_HANDLER': 'your_app.utils.errors.drf_exception_handler'
}
# REST_FRAMEWORK - EXCEPTION_HANDLER có tác dụng gì, dùng ở đâu, khi nào được dùng
```