
<cn>
#### 单选表格
- ta-big-table通过列设置type="radio"设置单选
- 单选表格，用户手动选中时会触发事件 radio-change
- ta-big-table可以通过 checkMethod 方法控制 radio 是否允许用户手动选中，还可以配置 labelField 列显示属性
- 单选表格默认选中，通过指定 checkRowKey 设置默认选中的行，指定默认值需要有 row-id（注：默认行为只会在 reload 之后触发一次）
</cn>

<us>
#### radio
radio
</us>

```html
<template>
  <div>
        <div style="margin-bottom: 10px">
            <ta-button @click="$refs.xTable.setRadioRow(tableData[0])">设置第一行选中（如果被禁用，不可选中）</ta-button>
            <ta-button @click="$refs.xTable.setRadioRow(tableData[1])">设置第二行选中</ta-button>
            <ta-button @click="clearRadioRowEevnt">取消选中</ta-button>
            <ta-button @click="getRadioEvent1">获取选中</ta-button>
        </div>
        <ta-big-table
          border
          ref="xTable"
          height="300"
          :data="tableData"
          :radio-config="{highlight: true,labelField: 'name', checkMethod: checkRadioMethod}"
          @cell-click="cellClickEvent"
          @radio-change="radioChangeEvent" >
          <ta-big-table-column type="radio" width="100">
            <template v-slot:header>
              <ta-button  size="small" @click="clearRadioRowEevnt" :disabled="!selectRow"> 取消</ta-button>
            </template>
          </ta-big-table-column>
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
              selectRow:false,
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
          },
          methods: {
            checkRadioMethod ({ row }) {
              return row.age > 26
            },
            cellClickEvent () {
              console.log('单元格点击事件')
            },
            radioChangeEvent ({ row }) {
              this.selectRow = row
              console.log('单选事件')
            },
            clearRadioRowEevnt () {
              this.selectRow = null
              this.$refs.xTable.clearRadioRow()
            },
            getRadioEvent1 () {
              message.info(JSON.stringify(this.$refs.xTable.getRadioRecord()))
            }
          }
        }
</script>
```
