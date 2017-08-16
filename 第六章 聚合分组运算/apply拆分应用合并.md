# apply: 一般性的"拆分一应用一合并"






参考：[pandas_apply_operations_to_dataframes](https://chrisalbon.com/python/pandas_apply_operations_to_dataframes.html)


Pandas中的map(), apply()和applymap()的区别
将一个自定义的函数应用到Pandas的数据结构中可以使用map(), apply()或者applymap()，它们的区别在于应用的对象不同。
1. map() 是一个Series的函数，DataFrame结构中没有map()。map()将一个自定义函数应用于Series结构中的每个元素(elements)。
2. apply()和applymap()是DataFrame结构中的函数，Series中没有。它们的区别在于，apply()将一个函数作用于DataFrame中的每个行或者列，而applymap()是将函数做用于DataFrame中的所有元素(elements)。​

Summing up, apply works on a row / column basis of a DataFrame, applymap works element-wise on a DataFrame, and map works element-wise on a Series.

参考：[difference-between-map-applymap-and-apply-methods-in-pandas](https://stackoverflow.com/questions/19798153/difference-between-map-applymap-and-apply-methods-in-pandas)
