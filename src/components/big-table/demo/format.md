
<cn>
#### 格式化内容
- big-table-column 可通过自定义 formatter 格式化单元格内容
（注：formatter 只会在指定的 field 值发生改变时触发格式化，如果想要多字段关联变化请使用自定义模板）
- 全局格式化内容，使用 formats 添加格式函数，单元格会在渲染的时候自动调用
  - 默认提供的格式化方法：
    - formatDate: 格式化日期，默认 yyyy-MM-dd HH:mm:ss
    - formatAmount: 格式化金额，每隔3位逗号分隔，默认2位小数
    - formatBankcard：格式化银行卡，默认每4位空格隔开
    - formatFixedNumber：四舍五入,默认两位小数
    - formatCutNumber：向下舍入,默认两位小数
    - toMomentString：转换 moment 类型为字符串
  - 自定义全局格式化函数：formatterName({cellValue, row, column})，<span style="color: red">如需传递参数，则在依次排列在第一个参数之后，传递时使用数组传递要调用的函数名和除第一个参数之外的其余参数，如本例的“format，带参数”列所示</span>
    ```
    import TaBigTable from '@yh/ta404-ui/es/big-table'
    // 添加一个方法
    TaBigTable.formats.add('customFormatNumber', ({ cellValue, }) => {
      return 'cunstom: ' + cellValue
    })
    // 混入多个方法
    TaBigTable.formats.mixin({
      format1: ({cellValue, row, column}, ...args) => {
      },
      format2: ({cellValue, row, column}, ...args) => {
      },
    })
    // 获取自定义format方法
    TaBigTable.formats.get('format1')
    // 删除自定义方法
    TaBigTable.formats.delete('format1')
    ```
</cn>

<us>
#### formatter
formatter
</us>

```html
<template>
  <div>
    <ta-big-table
          border
          :data="tableData">
          <ta-big-table-column type="seq" width="60"></ta-big-table-column>
          <ta-big-table-column field="name" title="Name" sortable></ta-big-table-column>
          <ta-big-table-column field="num" title="vue文件内format" :formatter="formatterNum" sortable></ta-big-table-column>
          <ta-big-table-column field="num8" title="全局自定义format" formatter="customFormatNumber" sortable></ta-big-table-column>
          <ta-big-table-column field="num9" title="默认format" formatter="formatFixedNumber" sortable></ta-big-table-column>
          <ta-big-table-column field="num10" title="format，带参数" :formatter="['formatFixedNumber', 3]" sortable></ta-big-table-column>
          <ta-big-table-column field="sex" title="Sex" collectionType="SEX" sortable></ta-big-table-column>
          <ta-big-table-column field="time" title="Time" formatter="formatDate"></ta-big-table-column>
        </ta-big-table>
  </div>
</template>
<script >
// 在入口文件将全局自定义format函数添加进去,示例如下代码
//import TaBigTable from '@yh/ta404-ui/es/big-table'
//TaBigTable.formats.add('customFormatNumber', ({ cellValue, }) => {
//  return 'cunstom: ' + cellValue
//})
       export default {
          data () {
            return {
              tableData: [
                { id: 10001, name: 'Test1', bankCard: '6222525678789432', sex: '0', time: 1599320111520, date: '2020-11-14T07:14:41.000Z', amount: 998.3, num: 863.345, num7: 863.345, num8: 863.345, num9: 863.345, num10: 863.345 },
                { id: 10002, name: 'Test2', bankCard: '6222525675674564', sex: '1', time: 1590820967410, date: '2022-10-24T08:14:18.000Z', amount: 777776536.3, num: 854.7789, num7: 854.7789, num8: 854.7789, num9: 854.7789, num10: 854.7789 },
                { id: 10003, name: 'Test3', bankCard: '6222525477686963', sex: '0', time: 1599390785410, date: '2020-09-04T06:08:25.000Z', amount: 253.486, num: 963.1456, num7: 963.1456, num8: 963.1456, num9: 963.1456, num10: 963.1456 },
                { id: 10004, name: 'Test4', bankCard: '6222525678678946', sex: '1', time: 1597385230710, date: '2019-10-20T20:40:20.000Z', amount: 9990000.66, num: 963.9856, num7: 963.9856, num8: 963.9856, num9: 963.9856, num10: 963.9856 },
                { id: 10005, name: 'Test5', bankCard: '6222525478909009', sex: '0', time: 1591627586920, date: '2020-09-17T11:14:18.000Z', amount: 10000.35, num: 99.845632, num7: 99.845632, num8: 99.845632, num9: 99.845632, num10: 99.845632 },
                { id: 10006, name: 'Test6', bankCard: '6222525789898793', sex: '1', time: 1599728569710, date: '2021-01-04T10:12:18.000Z', amount: 999, num: 698.3689, num7: 698.3689, num8: 698.3689, num9: 698.3689, num10: 698.3689 },
                { id: 10007, name: 'Test7', bankCard: '6222525476534534', sex: '1', time: 1590740052710, date: '2020-08-10T08:14:18.000Z', amount: 458666.3, num: 1000.3658, num7: 1000.3658, num8: 1000.3658, num9: 1000.3658, num10: 1000.3658 },
                { id: 10008, name: 'Test8', bankCard: '6222525445554231', sex: '0', time: 1599320425610, date: '2020-05-04T07:17:30.000Z', amount: 79999935.6, num: 600053.32845, num7: 600053.32845, num8: 600053.32845, num9: 600053.32845, num10: 600053.32845 }
              ],
              sexList: [
                {
                  label: '女',
                  value: '0'
                },
                {
                  label: '男',
                  value: '1'
                }
              ]
            }
          },
          methods: {
            formatterNum ({ cellValue }) {
              return cellValue
            },
          }
        }
</script>
```
