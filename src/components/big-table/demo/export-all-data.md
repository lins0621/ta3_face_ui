
<cn>
#### 导出数据
ta-big-table提供导出数据功能
- ta-big-table通过exportConfig配置导出功能
- ta-big-table要导出所有页的数据需要通过export-config配置exportMethod自定义导出。
    - 设置export-config中属性{remote:true,exportMethod: 自定义导出函数}
</cn>

<us>
#### export all data
- The export function on the toolbar needs to export all paged page data.
- To export data for all pages, you need to use a custom export
    - Set the property {remote:true, exportmethod: XXX function} in export-config
</us>

```html
<template>
  <div>
    <ta-big-table
            ref="bigTable"
            border
            show-overflow
            highlight-hover-row
            height="300"
            :export-config="exportConfig"
            :import-config="{}"
            :sort-config="{trigger: 'cell'}"
            :data="userList"
    >
      <ta-big-table-column type="checkbox" width="60" />
      <ta-big-table-column type="seq" width="60" />
      <ta-big-table-column field="name" title="name" sortable />
      <ta-big-table-column field="sex" title="Sex" />
      <ta-big-table-column field="loginId" title="账号" />
      <ta-big-table-column field="namePath" title="组织路径" show-overflow />
      <template #topBar>
      <ta-big-table-toolbar
              :import="true"
              :export="true"
              :print="true"
              :custom="true"
      >
        <div slot="buttons">
          <ta-button >新增</ta-button>
          <ta-button >删除</ta-button>
        </div>
        <div slot="tools">
          <ta-button >其他工具</ta-button>
          <ta-button >其他功能</ta-button>
        </div>
      </ta-big-table-toolbar>
      </template>
      <template #bottomBar>
        <ta-pagination
                ref="gridPager"
                style="text-align: right;margin-top: 10px"
                :data-source.sync="userList"
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
        userList: [],
          exportConfig: {mode:'all',modes:['current','selected','all'],remote:true,exportMethod: this.customExport},
      }
    },
    mounted(){
      //进入页面后默认查询表格第一页(分页条实例提供了loadData方法会默认查询第一页,并将数据渲染入表格)
      this.$refs.gridPager.loadData()
    },
    methods: {
      customExport (option) {
        console.log(option)
        if (option.options.mode === 'all') {
          return new Promise((resolve, reject) => {
            // 请求后端获得所有数据
            Base.submit(null, {
              url: 'http://172.20.23.216:8081/ta404/demo/tableRestService/queryUserByCondition',
              data: {
                pageNumber: 1,
                pageSize: 20,
              },
            }, {
              successCallback:(data) => {
                resolve(data)
              },
            })

          }).then(data => {
            // 通过请求获取到全部数据
            console.log('所有页数据', data)
            // 手动导出全部数据
            this.$refs.bigTable.exportData({
              ...option.options,
              remote: false,
              data: data.data.pageBean.list,
            })
          })
        } else {
          // 不是导出所有页情况
          return new Promise(resolve => {
            this.$refs.bigTable.exportData({
              ...option.options,
              remote: false,
            })
          })
        }
      },
    },
  }
</script>
```
