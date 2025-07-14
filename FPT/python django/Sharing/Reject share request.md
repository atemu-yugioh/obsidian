
Input

```python
{
    "id": "70c5bb0e11c743f5ad4eff1754d83b8b"
}
```

- kiểm tra request tồn tại với (status = pending)
- kiểm tra nếu là thực sự đúng là sharer thì cho update status thành reject và xóa thông báo trong notification hub
- kiểm tra nếu là thằng owner reject thì xóa request luôn
- pass hết thì update status thành **reject**