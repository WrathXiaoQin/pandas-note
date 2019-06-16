# pandas-note

##读取文件
```python
frame=pd.read_excel(r'C:\Users\wrath\Desktop\成交单报表.xls',skiprows=1,dtype={'流量编号':object})
frame=pd.read_csv(f,dtype={'编号':object,'推广站点':object},index_col=False)
```
## 合并表
```python
frame=pd.concat(files,ignore_index=True)
```
## 删除列
```python
frame.drop(['Unnamed: 64'],axis=1,inplace=True)
```
## 字段替换更改
```python
frame['呼叫军团名称']=frame['呼叫军团名称'].str.replace('\(老\)','')
frame.loc[frame['流量编号']=='345249634983084032','课程咨询师']='吴冰清'
```
## 插入列
```python
frame.insert(5, '销售组', frame['销售组2'])
```
## 写入excel
```python
writer=pd.ExcelWriter(path+'合并.xlsx')
frame.to_excel(writer,'合并',index=False)
writer.save()
```
## 转成值
```python
frame1['事业部'][-1:].values[0]--最后一个值
excel['事业部'].unique().tolist()--转成列表
```
## 条件筛选
```python
frame=frame.loc[(frame['状态']!='REVOKED')&(frame['状态']!='UNPAID')]--多条件合
frame=frame[(frame['军团']=='第八军团')|(frame['军团']=='第八军团-AA')]--多条件或
data=data[data['支付方式'].str.contains('转班留存')]--单条件包含
frame=frame[frame['时间']!='合计']--不包含某个值
```
## 函数
```python
frame['报名日期']=frame['报名时间'].apply(lambda x:x[:10])--单个参数
def function(a, b):
    if (a=="无限" or a=="乌尔肯" or a=="无限+") and b in("第八军团","第八军团-AA","第八军团-AA(老)","第八军团-A","第十五军团-A0","第十三军团","原第十三军团","第三十四军团","第四十一孵化器","第五十九孵化器","第三十孵化器","第二十三孵化器","D105孵化器"):
        return "墨提斯"
    elif a=="无限" or a=="乌尔肯" or a=="无限+":
        return "乌尔肯"
    else:
        return a
frame['事业部*']=frame.apply(lambda x: function(x['事业部'],x['军团']),axis=1)--多个参数
```
## 空值填充
```python
frame['销售组']=frame['销售组'].fillna("其他")
```
## 排序输出
```python
data=frame.groupby('事业部*')['流水(万)'].sum().sort_values(ascending=False).round(1)
```
## join用法
```python
frame3=pd.merge(frame, data, how='left', left_on=['站点ID','时间'], right_on=['站点ID','报名日期'])
```
