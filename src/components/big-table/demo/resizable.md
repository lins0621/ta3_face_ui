
<cn>
#### 列宽拖动
`ta-big-table`通过设置 resizable 属性启用列宽拖动功能
</cn>

<us>
#### resizable
resizable
</us>

```html
<template>
         <ta-big-table
           resizable
           :data="tableData">
           <ta-big-table-column type="seq" width="60"></ta-big-table-column>
           <ta-big-table-column field="name" title="Name"></ta-big-table-column>
           <ta-big-table-column field="sex" title="Sex"></ta-big-table-column>
           <ta-big-table-column field="age" title="Age"></ta-big-table-column>
           <ta-big-table-column field="address" title="Address" show-overflow></ta-big-table-column>
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
