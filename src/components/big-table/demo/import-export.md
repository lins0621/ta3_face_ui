
<cn>
#### 手动导入/导出
ta-big-table导入导出功能已经集成到了工具栏上,如果是基础使用建议直接使用工具栏的导入/导出,使用十分方便<br>
如果需要手动调用调入导出,那么需要自己手动调用方法实现
- ta-big-table手动调用导入数据：
    - 通过 importData 函数可以直接将数据导入表格中
- ta-big-table手动调用导出数据:
    - 通过调用 exportData 函数指定 type='csv' 可以直接将表格导出为 CSV/HTML/XML/TXT/XLS/XLSX 格式的文件；
    - 配置 columnFilterMethod 参数过滤指定列
    - 配置 dataFilterMethod 参数过滤指定行
    - 默认会排除 field 为空和 type 相关的功能列，可以通过自定义 data 和 columns 导出数据
    - 对于 csv 等特殊类型，可以通过设置 cell-type 将数值类型转为字符串类型
    - 只支持基本数据结构，目前不支持分组、合并等；树结构和虚拟滚动只允许导出数据源，前端导出的数据量有限，建议使用后端导出
    - 如果是服务端导出，通过设置 remote 和 exportMethod 开启服务端自定义导出
    - export-config配置isPrint参数设置高级导出是否出现打印按钮
    - 对于xls/xlsx的导出, 传入的对象与excel-util的[generateExcelByTable](process.env.VUE_APP_PUBLIC_PATH/components/excel-util-cn/#generateExcelByTable)函数的第二个参数完全一致
</cn>

<us>
#### import export
import export
</us>

```html
<template>
  <div>
     <ta-big-table
          border
          height="400"
          ref="xTable"
          :export-config="{isPrint:true}"
          :import-config="{}"
          :data="tableData">
          <template #topBar>
           <ta-button @click="clearDataEvent">清空数据</ta-button>
           <ta-button @click="importDataEvent">导入数据(自动识别导入文件的格式)</ta-button>
           <ta-button @click="exportDataEvent">导出数据</ta-button>
           <ta-button @click="exportDataEventXls">导出数据(xls)</ta-button>
           <ta-button @click="exportDataEventXlsx">导出数据(xlsx)</ta-button>
            <ta-button @click="exportSelectEvent">导出选中</ta-button>
            <ta-button @click="openExportEvent">高级导出</ta-button>
            <ta-button @click="exportFilterEvent">导出指定列 [name,sex]</ta-button>
            <ta-button @click="exportFilterRowEvent">导出sex=1的行</ta-button>
             <ta-button @click="exportSelfDataEvent">自定义数据导出</ta-button>
             <ta-button @click="exportBackDataEvent">导出后端获取到的数据</ta-button>
          </template>
          <ta-big-table-column type="checkbox" width="60"></ta-big-table-column>
          <ta-big-table-column type="seq" width="60"></ta-big-table-column>
          <ta-big-table-column field="name" title="Name" sortable></ta-big-table-column>
          <ta-big-table-column field="sex" title="Sex"  collection-type="SEX"></ta-big-table-column>
        <ta-big-table-column field="loginId" title="账号" />
         <ta-big-table-column field="namePath" title="组织路径" show-overflow />
                <template #bottomBar>
                    <ta-pagination
                      ref="gridPager"
                      style="text-align: right;"
                      :data-source.sync="tableData"
                      url="demo/tableRestService/queryUserByCondition"
                    />
                </template>
        </ta-big-table>
  </div>
</template>
<script>
 export default {
          data () {
            return {
              loading: false,
              tableData:[]
            }
          },
         mounted(){
           this.$refs.gridPager.loadData()
          },
          methods: {
            clearDataEvent () {
              this.tableData = []
            },
            // 手动导入
           importDataEvent () {
             this.$refs.xTable.importData()
           },
          // 手动导出
           exportDataEvent () {
              this.$refs.xTable.exportData({ type: 'csv',name:'csv' })
            },
            // 导出xls文件
            exportDataEventXls(){
              this.$refs.xTable.exportData({
                fileType: '.xls', // fileType在传入type的时候可以
                fileName: 'xls',
                sheetName: '一个sheet', // 可以自定义当前的sheet名称
                header: {
                  col: ['checkbox', 'seq', 'name', 'sex', 'loginId', 'namePath'], // 列说明，若未传入列说明，且表格数据为空将会报错
                  columns: [{ seq: '#', name: 'Name', sex: 'Sex', loginId: '账号', namePath: '组织路径', }],
                  exclude: ['action'], // 排除列
                },
              })
              // 等同于如下代码
              // generateExcelByTable(this.$refs.xTable.$el.querySelector('.vxe-table--main-wrapper .vxe-table--body-wrapper table'), {
              //   fileType: '.xls', // fileType在传入type的时候可以
              //   fileName: 'xls',
              //   header: {
              //     col: ['checkbox', 'seq', 'name', 'sex', 'loginId', 'namePath'], // 列说明，若未传入列说明，且表格数据为空将会报错
              //     columns: [{ seq: '#', name: 'Name', sex: 'Sex', loginId: '账号', namePath: '组织路径', }],
              //     exclude: ['checkbox'], // 排除列
              //   },
              // })
            },
            // 导出xlsx文件
            exportDataEventXlsx(){
              this.$refs.xTable.exportData({
                fileType: '.xlsx', // fileType在传入type的时候可以
                fileName: 'xlsx',
                header: {
                  col: ['checkbox', 'seq', 'name', 'sex', 'loginId', 'namePath'], // 列说明，若未传入列说明，且表格数据为空将会报错
                  columns: [{ seq: '#', name: 'Name', sex: 'Sex', loginId: '账号', namePath: '组织路径', }],
                  exclude: ['action'], // 排除列
                },
              })
              // 等同于如下代码
              // generateExcelByTable(this.$refs.xTable.$el.querySelector('.vxe-table--main-wrapper .vxe-table--body-wrapper table'), {
              //   fileType: '.xlsx', // fileType在传入type的时候可以
              //   fileName: 'xlsx',
              //   header: {
              //     col: ['checkbox', 'seq', 'name', 'sex', 'loginId', 'namePath'], // 列说明，若未传入列说明，且表格数据为空将会报错
              //     columns: [{ seq: '#', name: 'Name', sex: 'Sex', loginId: '账号', namePath: '组织路径', }],
              //     exclude: ['checkbox'], // 排除列
              //   },
              // })
            },
          // 手动导出选中
            exportSelectEvent () {
              this.$refs.xTable.exportData({
                data: this.$refs.xTable.getCheckboxRecords()
              })
            },
          // 高级导出,显示导出面板
            openExportEvent () {
              this.$refs.xTable.openExport({ isPrint: false })
            },
           // 导出配置的列
            exportFilterEvent () {
             this.$refs.xTable.exportData({
               type: 'csv',
               columnFilterMethod ({ column }) {
                 return ['name', 'sex'].includes(column.property)
               }
             })
           },
            // 导出配置的行
            exportFilterRowEvent () {
              this.$refs.xTable.exportData({
                type: 'csv',
                dataFilterMethod ({ row }) {
                  return row.sex === '1'
                }
              })
            },
          // 导出自定义数据信息
           exportSelfDataEvent(){
                 this.$refs.xTable.exportData({
                filename: '自定义文件名',
                type: 'html',
                isHeader: true,
                isFooter: true,
                // 自定义导出的数据源
                data: [
                  { name: 'Name1', sex: '男', age: 26, role: '前端', html1: '<a>xxx1</a>' },
                  { name: 'Name2', sex: '女', age: 20, role: '测试', html1: '<a>xxx2</a>' },
                  { name: 'Name4', sex: '女', age: 22, role: '设计师', html1: '<a>xxx3</a>' }
                ]
              })
             },
           // 导出从后端获取到的数据
           exportBackDataEvent(){
             Base.submit(null,{url:'demo/tableRestService/queryUserByCondition'}).then(data => {
                this.$refs.xTable.exportData({
                  filename: '自定义文件名',
                  type: 'csv',
                  isHeader: true,
                  isFooter: true,
                  data:data.data.pageBean.list
                })
              }).catch(() => {
                message.error('导出错误')
              })
           }
          }
        }
</script>
```
