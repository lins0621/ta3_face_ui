
<cn>
#### 常用事件
ta-big-table支持多种事件绑定包括 header-cell-click表头单元格单击,header-cell-dblclick表头单元格双击,cell-click单元格单击,cell-dblclick单元格双击,
cell-mouseenter单元格鼠标移入,cell-mouseleave单元格鼠标离开,scroll滚动条滚动等
</cn>

<us>
#### event
event
</us>

```html
<template>
  <div>

        <ta-big-table
          border
          highlight-hover-row
          show-overflow
          resizable
          height="400"
          :context-menu="{}"
          :data="tableData"
          @header-cell-click="headerCellClickEvent"
          @header-cell-dblclick="headerCellDBLClickEvent"
          @cell-click="cellClickEvent"
          @cell-dblclick="cellDBLClickEvent"
          @cell-mouseenter="cellMouseenterEvent"
          @cell-mouseleave="cellMouseleaveEvent"
          @scroll="scrollEvent">
          <ta-big-table-column type="seq" title="序号" width="60" fixed="left"></ta-big-table-column>
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
                { id: 10004, name: 'Test4', role: 'Designer', sex: 'Women ', age: 23, address: 'ta-big-table 从入门到放弃' },
                { id: 10005, name: 'Test5', role: 'Develop', sex: 'Women ', age: 30, address: 'Shanghai' },
                { id: 10006, name: 'Test6', role: 'Designer', sex: 'Women ', age: 21, address: 'ta-big-table 从入门到放弃' },
                { id: 10007, name: 'Test7', role: 'Test', sex: 'Man ', age: 29, address: 'ta-big-table 从入门到放弃' },
                { id: 10008, name: 'Test8', role: 'Develop', sex: 'Man ', age: 35, address: 'ta-big-table 从入门到放弃' }
              ]
            }
          },
          methods: {
            headerCellClickEvent ({ column }) {
              console.log(`表头单元格点击${column.title}`)
            },
            headerCellDBLClickEvent ({ column }) {
              console.log(`表头单元格双击${column.title}`)
            },
            cellClickEvent ({ column }) {
              console.log(`单元格点击${column.title}`)
            },
            cellDBLClickEvent ({ column }) {
              console.log(`单元格双击${column.title}`)
            },
            cellMouseenterEvent ({ column }) {
              console.log(`鼠标进入单元格${column.title}`)
            },
            cellMouseleaveEvent ({ column }) {
              console.log(`鼠标离开单元格${column.title}`)
            },
            scrollEvent ({ scrollTop, scrollLeft }) {
              console.log(`滚动事件scrollTop=${scrollTop} scrollLeft=${scrollLeft}`)
            }
          }
        }
</script>
```
