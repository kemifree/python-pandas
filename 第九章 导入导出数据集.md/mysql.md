# mysql 操作

## 操作方式一
```python

def get_table(db_name,db_table):
    con = 'mysql+pymysql://step:123456@172.16.57.72/'+ db_name+'?charset=utf8'
    engine = create_engine(con)
    #engine = create_engine("mysql+pymysql://step:123456@172.16.57.72/tmall?charset=utf8")
    sql = 'select * from '+  db_table
    table = pd.read_sql(sql,con=engine)
    #去除重复值
    return table   
table = get_table(db_name =db_name,db_table =db_table)

```
## 操作方式二：
```python
conn = pymysql.connect(host='172.16.57.72',
                             port=3306,
                             user='step',
                             password='123456',
                             db='tb_orders',
                             charset='utf8',
                             cursorclass=pymysql.cursors.DictCursor)
##读取数据方式一                    
cursor = conn.cursor()
sql =  'select * from temp_0209_01 '
cursor.execute(sql)
data = cursor.fetchall()
table = pd.DataFrame(data)
##读取数据方式2
import pandas as pd
from sqlalchemy import create_engine
engine = create_engine("mysql+pymysql://step:123456@172.16.57.72/tb_orders?charset=utf8")
sql = 'select taobaoshopname,uid  from  tbcrm limit 100 '
table = pd.read_sql(sql,con=engine)
#导入到mysql中
sheet.to_sql('tbcrmorder_orderstatus_2016',con=engine,if_exists='replace',index=False,chunksize=10000)

```

## python 调用mysql存储过程
```python
# -*- coding: utf-8 -*-
"""
Created on Thu Aug  3 14:59:11 2017
#it存储过程更新
@author: Administrator
"""
import time
import pymysql
from datetime import datetime, timedelta


def tb_user_procedure(procedure_name,params):
    start_time = time.time() # 开始时间
    conn = pymysql.connect(host='172.16.76.132',
                                 port=3306,
                                 user='boqii_crm_user',
                                 password='Rj64b5EVIwNhyBHgb',
                                 db='tb_user',
                                 charset='utf8',
                                 cursorclass=pymysql.cursors.DictCursor)    
    cursor = conn.cursor()
    cursor.execute(procedure_name,params)
    cursor.close()
    conn.commit()
    conn.close()
    print(procedure_name+'存错过程执行完毕')
    end_time = time.time() #结束时间
    print("程序耗时%f秒." % (end_time - start_time))


if __name__ == "__main__":
    start_time = time.time() # 开始时间
    for i in [5,4,3,2,1]:
        date = (datetime.date(datetime.now()) - timedelta(days=i)).strftime('%Y-%m-%d')
        print(date)
        #---001---用户分析表--存储过程
        try:
            procedure = ['call tb_user(%s,%s,%s)',('2017-08-09',-30,0)]
            params = tuple([date,-30,0])
            procedure[1] = params
            tb_user_procedure(procedure[0],procedure[1])
        except:
            print(procedure+'更新失败')
        #---002---用户基础表--存储过程
        try:
            procedure = ['call tb_user_before_day(%s)',('2017-08-09')]
            params = tuple([date])
            procedure[1] = params
            tb_user_procedure(procedure[0],procedure[1])
        except:
            print(procedure+'更新失败')
    end_time = time.time() #结束时间
    print("程序耗时%f秒." % (end_time - start_time))      

```
