<cn>
#### 树形表格过滤
- ta-big-table树形表格过滤示例
</cn>

<us>
#### tree table filter
tree table filter
</us>

```html
<template>
  <div>
    <ta-big-table
      ref="xTable"
      max-height="600"
      :loading="loading"
      :data="tableData"
      :tree-config="{children: 'children'}">
      <ta-big-table-column field="name" title="名称" tree-node>
        <template slot="header" slot-scope="{ row }">
          <span>名称：</span>
          <ta-input style="display: inline-block;width: 80%;" v-model="filterName" type="type" placeholder="Filter" @keyup="searchEvent"/>
        </template>
      </ta-big-table-column>
      <ta-big-table-column field="size" title="大小" width="140"></ta-big-table-column>
      <ta-big-table-column field="type" title="类型" width="140"></ta-big-table-column>
      <ta-big-table-column field="date" title="修改日期" width="260"></ta-big-table-column>
    </ta-big-table>
  </div>
</template>
<script>
import TaUtils from '@yh/ta-utils'
export default {
  data () {
    return {
      filterName: '',
      loading: false,
      originData: [],
      tableData: []
    }
  },
  created () {
    this.loading = true
    setTimeout(() => {
      this.loading = false
      this.originData = TaUtils.clone(window.mockTreeData, true)
      this.handleSearch()
    }, 300)
  },
  methods: {
    handleSearch () {
      let filterName = TaUtils.toString(this.filterName).trim()
      if (filterName) {
        let options = { children: 'children' }
        let searchProps = ['name']
        this.tableData = TaUtils.searchTree(this.originData, item => searchProps.some(key => TaUtils.toString(item[key]).indexOf(filterName) > -1), options)
        // 搜索之后默认展开所有子节点
        this.$nextTick(() => {
          this.$refs.xTable.setAllTreeExpand(true)
        })
      } else {
        this.tableData = this.originData
      }
    },
    // 创建一个防反跳策略函数，调用频率间隔 500 毫秒
    searchEvent: TaUtils.debounce(function () {
      this.handleSearch()
    }, 500, { leading: false, trailing: true })
  }
}
</script>
```
