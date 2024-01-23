
<cn>
#### 序号
- `ta-big-table`可通过设置`type=seq` 开启序号列
- `ta-big-table`可通过`seq-config={startIndex}` 自定义起始序号 如`:seq-config={startIndex:100}` 序号100开始
</cn>

<us>
#### seq
seq
</us>

```html
<template>
     <ta-big-table
          border
          highlight-hover-row
          height="300"
          :data="tableData">
          <ta-big-table-column type="seq" title="序号" width="60"></ta-big-table-column>
          <ta-big-table-column field="name" title="Name" sortable></ta-big-table-column>
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
        { id: 10004, name: 'Test4', role: 'Designer', sex: 'Women ', age: 24, address: 'Shanghai' }
      ]
    }
  }
}
</script>
```
