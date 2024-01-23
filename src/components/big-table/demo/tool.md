
<cn>
#### 工具栏
ta-big-table内置工具栏ta-big-table-toolbar,提供以下几个功能
- import 导入
- export 导出
- print 打印
- fullscreen 全屏(注意,表格必须使用一个div包裹起来)
- custom 自定义显示隐藏哪些列
- 支持自定义左侧按钮slot=buttons
- 支持自定义右侧按钮slot=tools
</cn>

<us>
#### toolbar
toolbar
</us>

```html
<template>
    <div style="height: 400px">
      <div class="fit">
        <ta-big-table
          border
          stripe
          resizable
          highlight-hover-row
          height="auto"
          ref="xTable"
          :export-config="{}"
          :import-config="{}"
          :data="tableData">
          <template #topBar>
            <ta-big-table-toolbar
              :import="true"
              :export="true"
              :print="true"
              :custom="true"
              :fullscreen="true"
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
          <ta-big-table-column type="seq" width="60"></ta-big-table-column>
          <ta-big-table-column field="name" title="Name" sortable></ta-big-table-column>
          <ta-big-table-column field="sex" title="Sex"  collection-type="SEX"></ta-big-table-column>
          <ta-big-table-column field="address" title="Address" show-overflow></ta-big-table-column>
        </ta-big-table>
      </div>
       
    </div>
</template>
<script>
    export default {
        data () {
            return {
                loading: false,
                tableData:  [
                    { id: 10001, name: 'Test1', role: 'Develop', sex: '1', age: 28, address: 'ta-big-table 从入门到放弃' },
                    { id: 10002, name: 'Test2', role: 'Test', sex: '2', age: 22, address: 'Guangzhou' },
                    { id: 10003, name: 'Test3', role: 'PM', sex: '1', age: 32, address: 'Shanghai' },
                    { id: 10004, name: 'Test4', role: 'Designer', sex: '2', age: 23, address: 'ta-big-table 从入门到放弃' },
                    { id: 10005, name: 'Test5', role: 'Develop', sex: '1', age: 30, address: 'Shanghai' },
                    { id: 10006, name: 'Test6', role: 'Designer', sex: '2', age: 21, address: 'ta-big-table 从入门到放弃' },
                    { id: 10007, name: 'Test7', role: 'Test', sex: '1', age: 29, address: 'ta-big-table 从入门到放弃' },
                    { id: 10008, name: 'Test8', role: 'Develop', sex: '2', age: 35, address: 'ta-big-table 从入门到放弃' }
                ]
            }
        },
        methods: {
            successCallback (editColumnEnd) {
                // 返回最终的列情况，visible为是否显示
                console.log('点击确定的回调，确定后的列情况', editColumnEnd)
            },
        },
    }
</script>
```
