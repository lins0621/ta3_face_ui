<cn>
#### 码表/字典
ta-big-table-column使用`collectionType`属性指定该列的码表/字典类型
</cn>

<us>
#### collection type
collection type
</us>

```html
<template>
  <div>
     <ta-big-table
          border
          stripe
          resizable
          highlight-hover-row
          height="400"
          :checkbox-config="{labelField: 'id', highlight: true, range: true}"
          :data="tableData">
          <ta-big-table-column type="seq" width="60"></ta-big-table-column>
          <ta-big-table-column type="checkbox" title="ID" width="140"></ta-big-table-column>
          <ta-big-table-column field="name" title="Name" sortable></ta-big-table-column>
          <ta-big-table-column field="sex" title="Sex" :filters="sexList" :filter-multiple="false" collection-type="SEX"></ta-big-table-column>
          <ta-big-table-column
            field="age"
            title="Age"
            sortable
            :filters="[{label: '大于16岁', value: 16}, {label: '大于26岁', value: 26}, {label: '大于30岁', value: 30}]"
            :filter-method="filterAgeMethod"></ta-big-table-column>
          <ta-big-table-column field="address" title="Address" show-overflow></ta-big-table-column>
        </ta-big-table>
  </div>
</template>
<script>
 export default {
          data () {
            return {
              loading: false,
              tableData: [],
              sexList: [
                {
                  label: '女',
                  value: '2'
                },
                {
                  label: '男',
                  value: '1'
                }
              ]
            }
          },
          created () {
            setTimeout(() => {
              this.tableData = [
                { id: 10001, name: 'Test1', role: 'Develop', sex: '1', age: 28, address: 'ta-big-table 从入门到放弃' },
                { id: 10002, name: 'Test2', role: 'Test', sex: '2', age: 22, address: 'Guangzhou' },
                { id: 10003, name: 'Test3', role: 'PM', sex: '1', age: 32, address: 'Shanghai' },
                { id: 10004, name: 'Test4', role: 'Designer', sex: '2', age: 23, address: 'ta-big-table 从入门到放弃' },
                { id: 10005, name: 'Test5', role: 'Develop', sex: '1', age: 30, address: 'Shanghai' },
                { id: 10006, name: 'Test6', role: 'Designer', sex: '2', age: 21, address: 'ta-big-table 从入门到放弃' },
                { id: 10007, name: 'Test7', role: 'Test', sex: '1', age: 29, address: 'ta-big-table 从入门到放弃' },
                { id: 10008, name: 'Test8', role: 'Develop', sex: '2', age: 35, address: 'ta-big-table 从入门到放弃' }
              ]
            }, 500)
          },
          methods: {
            formatterSex ({ cellValue }) {
              return cellValue ? (cellValue === '1' ? '男' : '女') : ''
            },
            filterAgeMethod ({ value, row, column }) {
              return row.age >= value
            }
          }
        }
</script>
```
