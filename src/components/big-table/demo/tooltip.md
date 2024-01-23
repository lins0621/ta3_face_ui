
<cn>
#### 自定义单元格提示
- `ta-big-table`通过`tooltip-config`配置提示属性
- 通过`tooltip-config.enabled` 属性开启全表工具提示
- 通过`tooltip-config.contentMethod` 方法重写默认的提示内容，显示逻辑完全自定义控制，可以返回 null 使用默认的提示消息
- `ta-big-table-column`通过`title-help`设置标题的帮助提示消息
</cn>

<us>
#### tooltip
tooltip
</us>

```html
<template>
  <ta-big-table
          show-footer
          :footer-method="footerMethod"
          :tooltip-config="{enabled: true, contentMethod: showTooltipMethod}"
          :data="tableData">
          <ta-big-table-column type="seq" width="60"></ta-big-table-column>
          <ta-big-table-column field="name" title="名称" :title-help="{message: '自定义帮助提示信息'}"></ta-big-table-column>
          <ta-big-table-column field="role" title="角色" :title-help="{message: '自定义图标', icon: 'fa fa-bell'}"></ta-big-table-column>
          <ta-big-table-column field="date" title="Date"></ta-big-table-column>
          <ta-big-table-column field="rate" title="Rate">
            <template v-slot:header>
              <span>自定义标题</span>
            </template>
          </ta-big-table-column>
          <ta-big-table-column field="address" title="Address" width="160"></ta-big-table-column>
          <ta-big-table-column type="html" field="content" title="Content" width="200"></ta-big-table-column>
        </ta-big-table>
</template>
<script>
export default {
   data () {
     return {
       tableData: [
         { name: 'Test1', role: '前端', date: '2020-02-28', rate: 5, address: 'address1', content: 'xxxxx1换行换行11111111111' },
         { name: 'Test2', role: '后端', date: '2020-02-22', rate: 2, address: 'address2\ntooltip文本换行\n换行xx', content: 'xxxxx1换行换行2' },
         { name: 'Test3', role: '前端', date: '2020-01-01', rate: 0, address: 'address3\ntooltip文本换行\n换行xx', content: 'xxxxx1换行换行3333' },
         { name: 'Test4', role: '设计师', date: '2020-02-23', rate: 1, address: 'address4', content: 'xxxxx1换行换行4' },
         { name: 'Test5', role: '前端', date: '2020-01-20', rate: 3, address: 'address5\ntooltip文本换行\n换行xx', content: 'xxxxx1换行换行55' }
       ]
     }
   },
   methods:{
     showTooltipMethod ({ type, column, row, items, _columnIndex }) {
       const { property } = column
      // 重写默认的提示内容
       if (property === 'role' || property === 'date') {
         if (type === 'header') {
           return column.title ? '自定义标题提示内容：' + column.title : ''
         } else if (type === 'footer') {
           return items[_columnIndex] ? '自定义表尾提示内容：' + items[_columnIndex] : ''
         }
         return row[property] ? `自定义提示内容: ${row[property]}`: ''
       }
       // 其余的单元格使用默认行为
       return null
     },
     footerMethod ({ columns }) {
       const footerData = [
         columns.map((column, columnIndex) => {
           if (columnIndex === 0) {
             return '合计'
           }
           if (['date'].includes(column.property)) {
             return '2020-09-05'
           }
           if (['rate'].includes(column.property)) {
             return 999.8
           }
           return null
         })]
      return footerData
     }
   }
}
</script>
```
