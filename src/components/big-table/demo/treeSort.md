<cn>
#### 树形表格排序
- ta-big-table树形表格排序示例
</cn>

<us>
#### Tree table sort
Tree table sort
</us>

```html
<template>
  <div>
    <h3 style="margin-bottom: 20px">“修改日期”列深层同级排序：</h3>
    <ta-big-table
      max-height="600"
      :loading="loading"
      :data="tableData"
      :tree-config="{children: 'children'}"
      @sort-change="sortChangeEvent">
      <ta-big-table-column field="id" title="ID" width="80"></ta-big-table-column>
      <ta-big-table-column field="name" title="名称" tree-node></ta-big-table-column>
      <ta-big-table-column field="size" title="大小" width="140"></ta-big-table-column>
      <ta-big-table-column field="type" title="类型" width="140"></ta-big-table-column>
      <ta-big-table-column field="date" title="修改日期" width="260" sortable remote-sort></ta-big-table-column>
    </ta-big-table>
  </div>
</template>
<script >
import TaUtils from '@yh/ta-utils'
export default {
  data () {
    return {
      loading: false,
      originData: [],
      tableData: []
    }
  },
  created () {
    this.originData = TaUtils.toTreeArray(window.mockTreeData)
    this.findList()
  },
  methods: {
    // 模拟后台接口
    findList (order) {
      this.loading = true
      setTimeout(() => {
        this.loading = false
        // 将有关联的列表转成树结构
        if (order === 'asc') {
          this.tableData = TaUtils.toArrayTree(this.originData, { key: 'id', parentKey: 'parentId', sortKey: 'date', reverse: false })
        } else if (order === 'desc') {
          this.tableData = TaUtils.toArrayTree(this.originData, { key: 'id', parentKey: 'parentId', sortKey: 'date', reverse: true })
        } else {
          this.tableData = TaUtils.toArrayTree(this.originData, { key: 'id', parentKey: 'parentId' })
        }
      }, 300)
    },
    sortChangeEvent ({ column, property, order }) {
      this.findList(order)
    }
  }
}
</script>
```
