# pandas-note
~~~

##合并表
```python
frame=pd.concat(files,ignore_index=True)
```
##删除列
```python
frame.drop(['Unnamed: 64'],axis=1,inplace=True)
```
##字段替换
```python
frame['呼叫军团名称']=frame['呼叫军团名称'].str.replace('\(老\)','')
```
