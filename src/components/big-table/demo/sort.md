
<cn>
#### 排序
- ta-big-table通过给需要排序功能的列加上 sortable 属性可以支持排序，还可以通过设置 sort-by 多字段进行排序
- ta-big-table通过sort-config配置defaultSort设置默认排序、配置orders 设置自定义轮转顺序、通过配置 trigger 设置触发源
- ta-big-table如果是服务端排序，只需加上 remote-sort 和 sort-change 事件就可以实现
- ta-big-table可以通过调用 sort 方法实现手动排序
</cn>

<us>
#### sort
sort
</us>

```html
<template>
  <div>
       <div style="margin-bottom: 10px">
           <ta-button @click="$refs.xTable.sort('name', 'asc')">Name 升序</ta-button>
            <ta-button @click="$refs.xTable.sort('name', 'desc')">Name 降序</ta-button>
            <ta-button @click="$refs.xTable.clearSort()">清除排序</ta-button>
       </div>
        <ta-big-table
          border
          highlight-hover-row
          ref="xTable"
          height="300"
          :data="tableData"
          @sort-change="sortChangeEvent"
          :sort-config="{trigger: 'cell', defaultSort: {field: 'age', order: 'desc'}, orders: ['desc', 'asc', null]}">
          <ta-big-table-column type="seq" width="60"></ta-big-table-column>
          <ta-big-table-column field="name" title="Name" sortable></ta-big-table-column>
          <ta-big-table-column field="role" title="Role" sortable></ta-big-table-column>
          <ta-big-table-column field="sex" title="Sex" sortable></ta-big-table-column>
          <ta-big-table-column field="age" title="Age" sortable></ta-big-table-column>
          <ta-big-table-column field="address" title="指定字age段排序" sort-by="age" sortable></ta-big-table-column>
        </ta-big-table>
  </div>
</template>
<script >
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
            sortChangeEvent ({ column, property, order }) {
              console.info(property, order)
            }
          }
        }
</script>
```
