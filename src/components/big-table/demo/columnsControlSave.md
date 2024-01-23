
<cn>
#### 列控制保存状态
- ta-big-table列控制保存状态保存示例<br>
在一些情况下需要对当表格拖动之后的状态保存(保存到后端或者缓存到前端),
这里提供一个缓存到前端的示例,保存到后端的做法思路是一致的
</cn>

<us>
#### Columns Control save
In some cases, we need to save the state of the table after dragging (save to the backend or cache to the front-end),
Here is an example of caching to the front-end, and the approach of saving to the back-end is consistent
</us>

```html
<template>
  <div>
    <ta-button @click='resetCols'>
      从缓存中重置列排序
    </ta-button>

    <ta-big-table
      ref='xTable'
      border
      stripe
      resizable
      highlight-hover-row
      height='400'
      :export-config='{}'
      :import-config='{}'
      :control-column='showHiddenOrSortColumn'
      :data='tableData'
    >
      <ta-big-table-column field='seq' type='seq' width='60' />
      <ta-big-table-column field='name' title='Name' sortable />
      <ta-big-table-column field='sex' title='Sex' collection-type='SEX' />
      <ta-big-table-column field='address' title='Address' show-overflow>
        <template #header>
          Address自定义header
        </template>
      </ta-big-table-column>
      <ta-big-table-column field='abc' title='abc' show-overflow />
    </ta-big-table>
  </div>
</template>
<script>
import { createWebStorage, } from '@yh/ta-utils'

export default {
  data () {
    return {
      myTableStore: null,
      // 列编辑配置
      showHiddenOrSortColumn: {
        // 主题颜色
        themeColor: 'red',
        // 自定义的按钮图标
        icon: 'appstore',
        // 显示隐藏列配置
        showHiddenConfig: {
          open: true,
        },
        // 列拖拽排序配置
        columnSortConfig: {
          open: true,
        },
        // 点击确定的回调，传回列的列表
        successCallback: this.successCallback,
      },
      loading: false,
      tableData: [
        { id: 10001, name: 'Test1', role: 'Develop', sex: '1', age: 28, address: 'ta-big-table 从入门到放弃', },
        { id: 10002, name: 'Test2', role: 'Test', sex: '2', age: 22, address: 'Guangzhou', },
        { id: 10003, name: 'Test3', role: 'PM', sex: '1', age: 32, address: 'Shanghai', },
        { id: 10004, name: 'Test4', role: 'Designer', sex: '2', age: 23, address: 'ta-big-table 从入门到放弃', },
        { id: 10005, name: 'Test5', role: 'Develop', sex: '1', age: 30, address: 'Shanghai', },
        { id: 10006, name: 'Test6', role: 'Designer', sex: '2', age: 21, address: 'ta-big-table 从入门到放弃', },
        { id: 10007, name: 'Test7', role: 'Test', sex: '1', age: 29, address: 'ta-big-table 从入门到放弃', },
        { id: 10008, name: 'Test8', role: 'Develop', sex: '2', age: 35, address: 'ta-big-table 从入门到放弃', }
      ],
    }
  },
  mounted () {
    // 缓存表格列排序的配置放到本地存储中
    this.myTableStore = createWebStorage('myTableStore', { isLocal: true, })
    this.$nextTick(() => {
      this.resetCols()
    })
  },
  methods: {
    successCallback ({ resultColumnsList, }) {
      const obj = {}
      resultColumnsList.forEach((item, index) => {
        obj[item.property] = {
          visible: item.visible,
          property: item.property,
          sortIndex: index,
        }
      })
      // 列排序设置到缓存上(或者保存到后端也行)
      this.myTableStore.set('xTable', obj)
    },
    // 重置列顺序
    resetCols () {
      // 获取缓存的列信息
      const obj = this.myTableStore.get('xTable')
      if (obj) {
        const cols = Object.keys(obj).map(item => {
          const c = this.$refs.xTable.getColumnByField(item)
          c.visible = obj[item].visible
          c.sortIndex = obj[item].sortIndex
          return c
        })
        cols.sort((a, b) => {
          return a.sortIndex > b.sortIndex
        })
        // 重置列排序
        this.$refs.xTable.loadColumn(cols)
      }
    },
  },
}
</script>

```
