
<cn>
#### 单元格溢出省略
- ta-big-table可通过设置show-overflow 和 show-header-overflow 和 show-footer-overflow让单元格(内容/表头/表尾)内容溢出时显示为省略号
- `show-overflow`/`show-header-overflow`/`show-footer-overflow`值为ellipsis时,内容溢出时显示为省略号
- `show-overflow`/`show-header-overflow`/`show-footer-overflow`值为title时,内容溢出时显示为省略号并用原生 title 显示
- `show-overflow`/`show-header-overflow`/`show-footer-overflow`值为tooltip时,内容溢出时显示为省略号并用 tooltip 显示
</cn>

<us>
#### ellipsis
ellipsis
</us>

```html
<template>
        <ta-big-table
          show-footer
          highlight-hover-row
          :footer-method="footerMethod"
          :data="tableData1">
          <ta-big-table-column type="seq" width="60"></ta-big-table-column>
          <ta-big-table-column field="name" title="名称" show-overflow="ellipsis"></ta-big-table-column>
          <ta-big-table-column field="role" title="角色" show-overflow></ta-big-table-column>
          <ta-big-table-column field="date" title="标题溢出，显示为 tooltip xxxxxxxxxx" show-header-overflow show-overflow="title" show-footer-overflow></ta-big-table-column>
          <ta-big-table-column field="rate" title="Rate" show-header-overflow="title">
            <template v-slot:header>
              <span>标题显示原生 title ___________________________</span>
            </template>
          </ta-big-table-column>
          <ta-big-table-column field="address" title="不换行不换行不换行不换行不换行不换行不换行不换行不换行" width="160"></ta-big-table-column>
        </ta-big-table>
</template>
<script>
  export default {
          data () {
            return {
              tableData1: [
                { name: 'Test1', role: '前端', date: '内容显示原生 title', rate: 5, address: 'address1' },
                { name: '内容超出隐藏，不显示提示信息xxxxxxxxxxxxxxxxxxx', role: '后端', date: '2020-02-22', rate: 2, address: 'address2\ntooltip文本换行\n换行xx' },
                { name: 'Test3', role: '内容超出一行显示为 tooltip xxxxxxxxxxxxxx', date: '2020-01-01', rate: 0, address: 'address3\ntooltip文本换行\n换行xx' },
                { name: 'Test4', role: '设计师', date: '2020-02-23', rate: 1, address: 'address4' },
                { name: 'Test5', role: '前端', date: '2020-01-20', rate: 3, address: 'address5\ntooltip文本换行\n换行xx' }
              ]
            }
          },
          methods:{
            footerMethod ({ columns }) {
              const footerData = [
                columns.map((column, columnIndex) => {
                  if (columnIndex === 0) {
                    return '合计'
                  }
                  if (['date'].includes(column.property)) {
                    return '说明 xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
                  }
                  if (['rate'].includes(column.property)) {
                    return '不想换行不想换行不想换行不想换行不想换行不想换行不想换行不想换行'
                  }
                  return null
                })
              ]
              return footerData
            }
          }
        }

</script>
```
