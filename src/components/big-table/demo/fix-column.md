
<cn>
#### 固定列
- ta-big-table通过设置 fixed=left|right 来启用固定列,当横向内容过多时，将列固定在左右两侧
- 如果列宽足够的话，固定列不会浮动
</cn>

<us>
#### fix column
fix column
</us>

```html
<template>
    <div>
       <ta-big-table
          border="inner"
          show-overflow
          :data="tableData">
          <ta-big-table-column type="seq" width="60" fixed="left"></ta-big-table-column>
          <ta-big-table-column field="name" title="Name" width="300"></ta-big-table-column>
          <ta-big-table-column field="role" title="Role" width="300"></ta-big-table-column>
          <ta-big-table-column field="sex" title="Sex" width="300"></ta-big-table-column>
          <ta-big-table-column field="date" title="Date" width="300"></ta-big-table-column>
          <ta-big-table-column field="address" title="Address" fixed="right" width="300"></ta-big-table-column>
        </ta-big-table>
    </div>
</template>
<script>
        export default {
          data () {
            return {
              tableData: [
                { id: 10001, name: 'Test1', role: 'Develop', sex: 'Man', age: 28, address: 'ta-big-table 从入门到放弃' },
                { id: 10002, name: 'Test2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou' },
                { id: 10003, name: 'Test3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai' },
                { id: 10004, name: 'Test4', role: 'Designer', sex: 'Women ', age: 24, address: 'Shanghai' }
              ]
            }
          }
        }
</script>
```
