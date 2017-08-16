# pymongo

## 向mongodb写入数据

```python
def insert_mongb(posts):
    from pymongo import MongoClient
    client = MongoClient('localhost', 27017)
    db = client.python
    table_phone = db.phone
    result = table_phone.insert_one(posts)
    return result

```

## 读取mongodb

```python
def read_mongb():
    from pymongo import MongoClient
    client = MongoClient('localhost', 27017)
    db = client.taobao
    taobao_product = db.taobao_product
    data = pd.DataFrame(pd.DataFrame(list(taobao_product.find())))

```
