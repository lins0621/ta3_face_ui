
<cn>
#### 展开子表格
- ta-big-table的展开子表格的示例
</cn>

<us>
#### expand table
expand table
</us>

```html
<template>
  <div style="height:400px">
       <ta-big-table
          border
          resizable
          height="100%"
          :data="tableData">
          <ta-big-table-column type="expand" width="80">
            <template v-slot:content="{ row }">
              <ta-big-table :data="row.children">
                        <ta-big-table-column type="seq" title="Sequence" ></ta-big-table-column>
                        <ta-big-table-column field="name" title="name"></ta-big-table-column>
                        <ta-big-table-column field="role" title="role"></ta-big-table-column>
                        <ta-big-table-column field="age" title="age"></ta-big-table-column>
                        <ta-big-table-column field="sex" title="sex"></ta-big-table-column>
             </ta-big-table>
            </template>
          </ta-big-table-column>
          <ta-big-table-column field="name" title="Name" ></ta-big-table-column>
          <ta-big-table-column field="size" title="Size"></ta-big-table-column>
          <ta-big-table-column field="type" title="Type"></ta-big-table-column>
          <ta-big-table-column field="date" title="Date"></ta-big-table-column>
        </ta-big-table>
  </div>
</template>
<script>
  export default {
          data () {
            return {
              tableData: [],
            }
          },
          created () {
            this.tableData = [
               {id: "10000", name: "ta-big-table 从入门到放弃 10000", size: "53k", type: "png",date:'2019-10-12',
                  children:[ { name: 'TEST1', role: 'Develop', age: 20, sex: '女' },
                        { name: 'TEST2', role: 'Develop', age: 22, sex: '女' },
                        { name: 'TEST3', role: 'Develop', age: 24, sex: '男' },
                        { name: 'TEST4', role: 'Develop', age: 26, sex: '女' },
                        { name: 'TEST5', role: 'Develop', age: 28, sex: '男' },
                        { name: 'TEST6', role: 'Develop', age: 30, sex: '男' }]},
               {id: "10001", name: "ta-big-table 从入门到放弃 10000", size: "53k", type: "png",date:'2019-10-12'},
               {id: "10002", name: "ta-big-table 从入门到放弃 10000", size: "53k", type: "png",date:'2019-10-12'},
               {id: "10003", name: "ta-big-table 从入门到放弃 10000", size: "53k", type: "png",date:'2019-10-12'},
               {id: "10004", name: "ta-big-table 从入门到放弃 10000", size: "53k", type: "png",date:'2019-10-12'},
               {id: "10005", name: "ta-big-table 从入门到放弃 10000", size: "53k", type: "png",date:'2019-10-12'},
              ]
          },
        }
</script>
```
