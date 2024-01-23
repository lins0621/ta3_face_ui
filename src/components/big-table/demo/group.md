<cn>
#### 表头分组/复杂表头
- 当数据结构比较复杂的时候，big-table可以使用多级表头big-table-colgroup来更加直观的显示数据
- ta-big-table固定列必须按组进行设置
- <span>注意：分组表头不支持横向虚拟滚动，设置 scroll-x={gt: -1} 关闭即可</span>
</cn>

<us>
#### group
group
</us>

```html
<template>
    <ta-big-table
          border
          height="400"
          :data="tableData">
          <ta-big-table-colgroup title="基本信息" fixed="left" >
            <ta-big-table-column type="seq" width="60"></ta-big-table-column>
            <ta-big-table-column field="name" title="Name" width="200"></ta-big-table-column>
          </ta-big-table-colgroup>
          <ta-big-table-colgroup title="更多信息" >
            <ta-big-table-column field="role" title="Role" width="200"></ta-big-table-column>
            <ta-big-table-colgroup title="详细信息">
              <ta-big-table-column field="sex" title="Sex" width="300"></ta-big-table-column>
              <ta-big-table-column field="age" title="Age" width="300"></ta-big-table-column>
            </ta-big-table-colgroup>
          </ta-big-table-colgroup>
          <ta-big-table-colgroup title="分类信息">
            <ta-big-table-column field="date3" title="Date" width="300"></ta-big-table-column>
          </ta-big-table-colgroup>
          <ta-big-table-column field="address" title="Address" show-overflow width="300"></ta-big-table-column>
        </ta-big-table>
</template>
<script>
        export default {
          data () {
            return {
              tableData: [
                { id: 10001, name: 'Test1', role: 'Develop', sex: 'Man', age: 28, address: 'ta-big-table 从入门到放弃' },
                { id: 10002, name: 'Test2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou' },
                { id: 10003, name: 'Test3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai' },
                { id: 10004, name: 'Test4', role: 'Designer', sex: 'Women ', age: 23, address: 'ta-big-table 从入门到放弃' },
                { id: 10005, name: 'Test5', role: 'Develop', sex: 'Women ', age: 30, address: 'Shanghai' },
                { id: 10006, name: 'Test6', role: 'Designer', sex: 'Women ', age: 21, address: 'ta-big-table 从入门到放弃' },
                { id: 10007, name: 'Test7', role: 'Test', sex: 'Man ', age: 29, address: 'ta-big-table 从入门到放弃' },
                { id: 10008, name: 'Test8', role: 'Develop', sex: 'Man ', age: 35, address: 'ta-big-table 从入门到放弃' }
              ]
            }
          }
        }

</script>
```
