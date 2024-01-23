
<cn>
#### 列宽
- ta-big-table通过设置 width 参数配置列宽度，支持固定像素、百分比、等比例分配等，如果不设置则按照表格的宽度进行均匀分配
- ta-big-table通过设置resizable属性允许列宽拖动
- <span style="color:red">(注：不应该全部都使用固定像素，应该当所有列加起来的宽度小于表格宽度时，就会出现空白区，可以配合 "%" 或 "min-width" 实现等比例缩放)</span></span>
</cn>

<us>
#### width
width
</us>

```html
<template>
        <ta-big-table
          border
          resizable
          :data="tableData">
          <ta-big-table-column type="seq"></ta-big-table-column>
          <ta-big-table-column field="name" title="Name(120px)" width="120px"></ta-big-table-column>
          <ta-big-table-column field="role" title="Role(20%)" width="20%"></ta-big-table-column>
          <ta-big-table-column field="sex" title="Sex"></ta-big-table-column>
          <ta-big-table-column field="date" title="Date"></ta-big-table-column>
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
