<cn>
#### 树形表格懒加载
- ta-big-table使用`tree-config`配置开启异步加载、子节点属性、叶子结点标志及加载方法，此示例同样展示了属性表格右键菜单的配置
</cn>

<us>
#### tree table async load
tree table async load
</us>

```html
<template>
  <div>
    <ta-big-table
      ref="xTree"
      border
      resizable
      row-id="id"
      :loading="loading"
      height="300px"
      :menu-config="{body: {options: bodyMenus}, visibleMethod}"
      :tree-config="{lazy: true, children: 'children', hasChild: 'hasChild', loadMethod: loadChildrenMethod}"
      :data="tableData"
      @menu-click="contextMenuClickEvent"
    >
      <ta-big-table-column field="orgName" title="组织名称" width="400" tree-node />
      <ta-big-table-column field="spell" title="组织拼音" />
      <ta-big-table-column field="orgType" title="组织类型" collection-type="ORGTYPE"/>
      <ta-big-table-column field="namePath" title="组织路径" />
    </ta-big-table>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loading: false,
      tableData: [],
      bodyMenus: [
        [
          {
            code: 'clearLoaded',
            name: '清除加载状态',
            disabled: false,
          },
          {
            code: 'reloadNodes',
            name: '重新加载子节点',
            disabled: false,
          },
          {
            code: 'expand',
            name: '展开节点',
            disabled: false,
          },
          {
            code: 'contract',
            name: '收起节点',
            disabled: false,
          }
        ]
      ],
    }
  },
  created () {
    this.findList()
  },
  methods: {
    findList () {
      this.loading = true
      Base.submit(null, {url: 'demo/tableRestService/queryTree', }).then(data => {
        this.tableData = data.data.orgTree.map(item => ({
          ...item,
          hasChild: item.childNum > 0,
        }))
        this.loading = false
      })
    },
    loadChildrenMethod ({ row, }) {
      return Base.submit(null, {url: 'demo/tableRestService/queryTree', data:{orgId: row.orgId, }, }).then((data) => {
        return Promise.resolve(data.data.orgTree.map(item => ({
          ...item,
          hasChild: item.childNum > 0,
        })))
      })
    },
    visibleMethod  ({ row, type, }) {
      let xTree = this.$refs.xTree
      if (type === 'body') {
        this.bodyMenus.forEach(list => {
          list.forEach(item => {
            if (['clearLoaded', 'reloadNodes'].includes(item.code)) {
              item.disabled = !row.hasChild || !xTree.isTreeExpandLoaded(row)
            } else if (['expand', 'contract'].includes(item.code)) {
              if (row.hasChild) {
                let isExpand = xTree.isTreeExpandByRow(row)
                item.disabled = ['expand'].includes(item.code) ? isExpand : !isExpand
              } else {
                item.disabled = true
              }
            }
          })
        })
      }
      return true
    },
    contextMenuClickEvent ({ menu, row, column, }) {
      let xTree = this.$refs.xTree
      switch (menu.code) {
        case 'clearLoaded':
          xTree.clearTreeExpandLoaded(row)
          break
        case 'reloadNodes':
          xTree.reloadTreeChilds(row)
          break
        case 'expand':
          xTree.setTreeExpand(row, true)
          break
        case 'contract':
          xTree.setTreeExpand(row, false)
          break
      }
    },
  },
}
</script>

```
