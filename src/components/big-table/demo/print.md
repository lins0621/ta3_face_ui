
<cn>
#### 手动打印
ta-big-table打印功能已经集成到了工具栏上,如果是基础使用建议直接使用工具栏的打印,使用十分方便<br>
如果需要手动调用调打印,那么需要自己手动调用方法实现
- 通过调用 print 函数打印表格 （注：打印的页数有限，如果超大数据量请关闭打印功能或者分页打印）
- 通过打印export-config配置isPrint参数设置高级打印是否出现打印按钮
</cn>

<us>
#### print
print
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
           <ta-button @click="exportDataEvent">打印数据</ta-button>
            <ta-button @click="exportSelectEvent">打印选中</ta-button>
            <ta-button @click="openExportEvent">高级打印</ta-button>
            <ta-button @click="exportFilterEvent">打印指定列 [name,sex]</ta-button>
            <ta-button @click="exportFilterRowEvent">打印sex=1的行</ta-button>
             <ta-button @click="exportSelfDataEvent">自定义数据打印</ta-button>
             <ta-button @click="exportBackDataEvent">打印后端获取到的数据</ta-button>
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
          // 手动打印
           exportDataEvent () {
              this.$refs.xTable.print({ sheetName:'csv' })
            },
          // 手动打印选中
            exportSelectEvent () {
              this.$refs.xTable.print({
                data: this.$refs.xTable.getCheckboxRecords()
              })
            },
          // 高级打印,显示打印面板
            openExportEvent () {
              this.$refs.xTable.openExport({ isPrint: true })
            },
           // 打印配置的列
            exportFilterEvent () {
             this.$refs.xTable.print({
               columnFilterMethod ({ column }) {
                 return ['name', 'sex'].includes(column.property)
               }
             })
           },
            // 打印配置的行
            exportFilterRowEvent () {
              this.$refs.xTable.print({
                dataFilterMethod ({ row }) {
                  return row.sex === '1'
                }
              })
            },
          // 打印自定义数据信息
           exportSelfDataEvent(){
                 this.$refs.xTable.print({
                sheetName: '自定义文件名',
                isHeader: true,
                isFooter: true,
                // 自定义打印的数据源
                data: [
                  { name: 'Name1', sex: '男', age: 26, role: '前端', html1: '<a>xxx1</a>' },
                  { name: 'Name2', sex: '女', age: 20, role: '测试', html1: '<a>xxx2</a>' },
                  { name: 'Name4', sex: '女', age: 22, role: '设计师', html1: '<a>xxx3</a>' }
                ]
              })
             },
           // 打印从后端获取到的数据
           exportBackDataEvent(){
             Base.submit(null,{url:'demo/tableRestService/queryUserByCondition'}).then(data => {
                this.$refs.xTable.print({
                  filename: '自定义文件名',
                  type: 'csv',
                  isHeader: true,
                  isFooter: true,
                  data:data.data.pageBean.list
                })
              }).catch(() => {
                message.error('打印错误')
              })
           }
          }
        }
</script>
```
