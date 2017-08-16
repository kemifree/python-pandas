# xlsx
```python
def read_xlsx(path,sheet_name):
    xlsx_file = pd.ExcelFile(path) ##路径
    xlsx_table = xlsx_file.parse(sheet_name) ##选取表格
    #写入excel
    xlsx_table.to_excel(path,sheet_name,index=False)
    return(xlsx_table)

```


## 从多个数据库查询结果并保存到excel
```python
import pandas as pd
from datetime import datetime
if __name__ == "__main__":
    month_date = datetime.date(datetime.now()).strftime('%Y-%m')
    print(u'现在的月份是' + str(month_date))
    table = '运营明细表'
    path = 'C:\\Users\\Acer\\Desktop\\运营明细表\\'
    boqii = '全店'
    download_path = path+boqii + table+'.xlsx'
    writer = pd.ExcelWriter(download_path)

    db = [{'server_db1':'name1'},
          {'server_db2':'name2'},
          {'server_db3':'name3'},
          {'server_db4':'name4'},
          {'server_db5':'name5'},
          {'server_db6':'name6'}]
    for i in db:
        for key in i:
            db_server = key
            db_name = i[key]
            df =search_table(db_server=db_server,table=table)
            #search_table 是自行编写的数据库查询函数，返回DataFrame
            file = db_name+'---'+table+'.xlsx'
            file_path = path+file
            df.to_excel(file_path,index=False)#每一个df保存单独保存excel文件；
            print('正在下载---'+db_name+'---'+table)
            #全部保存到一个excel文件中
            df.to_excel(writer,index=False,sheet_name=db_name)
    writer.save()

```
