
<cn>
#### 多选表格
- ta-big-table通过列设置type="checkbox"设置多选
- ta-big-table多选表格，用户手动勾选时会触发事件 checkbox-change
- ta-big-table可以通过 checkMethod 方法控制 checkbox 是否允许用户手动勾选，还可以配置 labelField 列显示属性
- ta-big-table还可以通过 strict 设置为严格模式，当表格中不存在有效数据时列头复选框为禁用状态
- ta-big-table多选表格，通过配置 trigger 设置触发源，使用渲染最快的 checkField 属性绑定方式
- ta-big-table默认选中，通过指定 checkRowKeys 设置默认选中的行，指定默认值需要有 row-id（注：默认行为只会在 reload 之后触发一次）
- ta-big-table可通过 range 启用范围选中
</cn>

<us>
#### checkbox
checkbox
</us>

```html
<template>
  <div>
       <div style="margin-bottom: 10px">
                   <ta-button @click="$refs.xTable1.toggleCheckboxRow(tableData[1])">切换第二行选中</ta-button>
                   <ta-button @click="$refs.xTable1.setCheckboxRow([tableData[2], tableData[3]], true)">设置第三、四行选中</ta-button>
                   <ta-button @click="$refs.xTable1.setAllCheckboxRow(true)">设置所有行选中</ta-button>
                   <ta-button @click="$refs.xTable1.clearCheckboxRow()">清除所有行选中</ta-button>
                   <ta-button @click="getSelectEvent">获取选中</ta-button>
       </div>
        <ta-big-table
          border
          ref="xTable1"
          :data="tableData"
          row-id="id"
          @checkbox-all="selectAllEvent"
          @checkbox-change="selectChangeEvent"
           :checkbox-config="{ checkMethod: checCheckboxkMethod2, trigger: 'row',checkRowKeys: defaultSelecteRows}">
          <ta-big-table-column type="checkbox" width="60"></ta-big-table-column>
          <ta-big-table-column field="name" title="Name"></ta-big-table-column>
          <ta-big-table-column field="sex" title="Sex"></ta-big-table-column>
          <ta-big-table-column field="age" title="Age"></ta-big-table-column>
          <ta-big-table-column field="address" title="Address" show-overflow></ta-big-table-column>
        </ta-big-table>
  </div>
</template>
<script>
         export default {
             data () {
               return {
                defaultSelecteRows:[10002, 10003],
                 tableData: [
                   { id: 10001, name: 'Test1', role: 'Develop', sex: 'Man', age: 28, address: 'ta-big-table 从入门到放弃' },
                   { id: 10002, name: 'Test2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou' },
                   { id: 10003, name: 'Test3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai' },
                   { id: 10004, name: 'Test4', role: 'Designer', sex: 'Women ', age: 23, address: 'ta-big-table 从入门到放弃' },
                   { id: 10005, name: 'Test5', role: 'Develop', sex: 'Women ', age: 30, address: 'Shanghai' }
                 ]
               }
             },
             methods: {
               selectAllEvent ({ checked, records }) {
                 console.log(checked ? '所有勾选事件' : '所有取消事件', records)
               },
               selectChangeEvent ({ checked, records }) {
                 console.log(checked ? '勾选事件' : '取消事件', records)
               },
               getSelectEvent () {
                 let selectRecords = this.$refs.xTable1.getCheckboxRecords()
                 message.info(selectRecords.length)
               },
              checCheckboxkMethod2 ({ row }) {
                return row.age > 26
              }
             }
           }
</script>
```
