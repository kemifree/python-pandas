## 选入观测

选入或剔除观测（行）是数据准备和数据分析的一个关键方面

## 布尔型数组选取行
* 方式一
![](assets/markdown-img-paste-20170813163221482.png)

* 方式二
![](assets/markdown-img-paste-20170813163615432.png)

## 切片操作
* 不推荐这种方式
![](assets/markdown-img-paste-20170813165533441.png)



## 删除指定轴上的数据

```df.drop(['column_1','columns_2'])```
默认 axis=0 删除rows数据

![](assets/markdown-img-paste-20170813164505543.png)

* 引申：若要删除指定columns，可以使用drop方法，但需传入axis=1
![](assets/markdown-img-paste-20170813164829133.png)
