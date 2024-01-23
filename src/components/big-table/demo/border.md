
<cn>
#### 边框
- 通过设置 border=false|default 默认显示边框
- 通过设置 border=true|full 显示完整边框
- 通过设置 border=outer 显示外边框
- 通过设置 border=inner 显示内边框
- 通过设置 border=none 去掉所有边框
</cn>

<us>
#### border
border
</us>

```html
<template>
  <div>
      <ta-radio-group v-model="border" style="margin-bottom:10px">
          <ta-radio value="default">default</ta-radio>
          <ta-radio value="full">full</ta-radio>
          <ta-radio value="outer">outer</ta-radio>
          <ta-radio value="inner">inner</ta-radio>
          <ta-radio value="none">none</ta-radio>
      </ta-radio-group>
        <ta-big-table
          height="200"
          :border="border"
          :data="tableData">
          <ta-big-table-column type="seq" width="60"></ta-big-table-column>
          <ta-big-table-column field="name" title="Name"></ta-big-table-column>
          <ta-big-table-column field="sex" title="Sex"></ta-big-table-column>
          <ta-big-table-column field="age" title="Age"></ta-big-table-column>
          <ta-big-table-column field="address" title="Address" show-overflow></ta-big-table-column>
        </ta-big-table>
  </div>
</template>
<script >
export default {
  data () {
    return {
      border:'',
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
