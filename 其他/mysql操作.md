
mysql 操作

```python
import sqlalchemy
from sqlalchemy.types import VARCHAR
#建立连接
engine=sqlalchemy.create_engine('mysql://root:mini123456@localhost:3306/tmall?charset=utf8',encoding='utf8')
##写入到数据库
data_ok.to_sql('product_orders_1111',con=engine,if_exists='replace',index=False,chunksize=1000,dtype={u'买家会员名':VARCHAR(length=255)})


```

```python
def write_sql_orders(data,db_table):
    try:
        table=data
        dtype={dtype:VARCHAR(length=255) for dtype in table.columns}
        dtype[u'address'] = VARCHAR(length=2550)
        dtype[u'taobaoUsername'] = VARCHAR(length=2550)
        dtype[u'taobaoTradeId'] = VARCHAR(length=2550)
        engine=sqlalchemy.create_engine('mysql://root:mini123456@localhost:3306/louis?charset=utf8',encoding='utf8')       
        table.to_sql(name=db_table,con=engine,flavor='mysql',if_exists='replace',index=False,chunksize=10000,dtype=dtype)   
        info =u'数据写入成功'
        print info
    except:
        info = u'数据写入失败'
        print info
    return info


```
