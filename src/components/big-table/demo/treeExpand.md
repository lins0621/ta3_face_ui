<cn>
#### 树形表格展开关闭 
- ta-big-table的树形表格支持树形展开行,通过`tree-config`属性配置树展开，使用`expandRowKeys`配置展开行，使用`expandAll: true`默认展开所有,使用`accordion: true`实现每次只展开一个同级节点
- ta-big-table-column使用`type="expand"`的列 + 名为`content`的插槽实现行详情展开，使用big-table的`expand-config`属性配置是否行详情展开懒加载，懒加载的函数需要返回一个`Promise`
</cn>

<us>
#### Base tree table
Base tree table
</us>

```html
<template>
    <div>
      <div style="margin-bottom: 20px">
        <ta-button @click="getTreeExpansionEvent">获取已展开</ta-button>
        <ta-button style="margin-left: 20px" @click="$refs.xTable.setAllTreeExpand(true)">展开所有</ta-button>
        <ta-button style="margin-left: 20px" @click="$refs.xTable.setAllTreeExpand(false)">关闭所有</ta-button>
      </div>
      <ta-big-table
        ref="xTable"
        height="300px"
        resizable
        row-id="id"
        :tree-config="{children: 'children', expandRowKeys: defaultExpandKeys}"
        :expand-config="{lazy: true, loadMethod: loadContentMethod}"
        :data="tableData"
        @toggle-tree-expand="toggleExpandChangeEvent">
        <ta-big-table-column field="name" title="Name" tree-node></ta-big-table-column>
        <ta-big-table-column type="expand" width="65" title="Details">
          <template slot="content" slot-scope="{ row }">
            <ul>
              <li>
                <span>ID：</span>
                <span>{{ row.id }}</span>
              </li>
              <li>
                <span>请求返回的属性1：</span>
                <span>{{ row.new1 }}</span>
              </li>
              <li>
                <span>请求返回的属性2：</span>
                <span>{{ row.new2 }}</span>
              </li>
            </ul>
          </template>
        </ta-big-table-column>
        <ta-big-table-column field="size" title="Size"></ta-big-table-column>
        <ta-big-table-column field="type" title="Type"></ta-big-table-column>
        <ta-big-table-column field="date" title="Date"></ta-big-table-column>
      </ta-big-table>
    </div>
</template>
<script>
export default {
  data () {
    return {
      tableData: [],
      defaultExpandKeys: [],
    }
  },
  created () {
    this.defaultExpandKeys = ['30000']
    this.tableData = mockTreeData
  },
  methods: {
    toggleExpandChangeEvent ({ row, expanded }) {
      console.log('节点展开事件' + expanded)
    },
    getTreeExpansionEvent () {
      let treeExpandRecords = this.$refs.xTable.getTreeExpandRecords()
      message.info(treeExpandRecords.length)
    },
    loadContentMethod ({ row }) {
      return new Promise(resolve => {
        row.new1 = `${Math.random().toFixed(2) * 100} - 模拟请求到的属性1`
        row.new2 = `${Math.random().toFixed(2) * 100} - 模拟请求到的属性2`
        // 模拟请求
        setTimeout(() => resolve(), 500)
      })
    }
  }
}
</script>
```
