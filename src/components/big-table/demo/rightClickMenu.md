<cn>
#### 右键菜单
- ta-big-table通过menu-config配置右键快捷菜单
- ta-big-table右键菜单,支持表头菜单、内容菜单、表尾菜单，通过 `visibleMethod` 和 `visible`、`disabled` 属性来控制菜单选项的操作权限
</cn>

<us>
#### context menu
context menu
</us>

```html
<template>
  <div>
    <ta-big-table
      ref="xTable"
      border
      show-footer
      highlight-current-row
      highlight-current-column
      :footer-method="footerMethod"
      :data="tableData"
      :menu-config="tableMenu"
      @header-cell-menu="headerCellContextMenuEvent"
      @footer-cell-menu="footerCellContextMenuEvent"
      @cell-menu="cellContextMenuEvent"
      @menu-click="contextMenuClickEvent"
    >
      <ta-big-table-column type="seq" width="60" />
      <ta-big-table-column field="name" title="Name" sortable />
      <ta-big-table-column field="sex" title="Sex" />
      <ta-big-table-column field="age" title="Age" />
      <ta-big-table-column field="time" title="Time" />
    </ta-big-table>
  </div>
</template>

<script >
import { mean, } from '@yh/ta-utils'
import {copyText,} from '@yh/ta-utils/clipboard'
export default {
  data () {
    return {
      tableData: [],
      tableMenu: {
        header: {
          options: [
            [
              { code: 'exportAll', name: '导出所有.csv', prefix: 'download', visible: true, disabled: false, }
            ]
          ],
        },
        body: {
          options: [
            [
              { code: 'details', name: '查看详情', prefixIcon: 'read', visible: true, disabled: false, }
            ],
            [
              { code: 'copy', name: '复制', prefixIcon: 'copy', visible: true, disabled: false, },
              { code: 'clear', name: '清除内容', prefixIcon: 'close', visible: true, disabled: false, }
            ],
            [
              { code: 'remove', name: '删除', prefixIcon: 'delete', visible: true, disabled: false, },
              {
                code: 'filter',
                name: '筛选',
                prefixIcon: 'filter',
                visible: true,
                disabled: false,
                children: [
                  { code: 'clearFilter', name: '清除筛选', visible: true, disabled: false, },
                  { code: 'filterSelect', name: '按所选单元格的值筛选', visible: true, disabled: false, }
                ],
              },
              {
                code: 'sort',
                name: '排序',
                prefixIcon: 'ordered-list',
                visible: true,
                disabled: false,
                children: [
                  { code: 'clearSort', name: '清除排序', prefixIcon: 'close', visible: true, disabled: false, },
                  { code: 'sortAsc', name: '升序', prefixIcon: 'sort-ascending', visible: true, disabled: false, },
                  { code: 'sortDesc', name: '倒序', prefixIcon: 'sort-descending', visible: true, disabled: false, }
                ],
              },
              { code: 'print', name: '打印', prefixIcon: 'printer', disabled: true, }
            ]
          ],
        },
        footer: {
          options: [
            [
              { code: 'clearAll', name: '清空数据', visible: true, disabled: false, }
            ]
          ],
        },
        visibleMethod: this.visibleMethod,
      },
    }
  },
  created () {
    this.tableData = [{
      name: 'Nick',
      sex: '男',
      age: '13',
      time: '2020-11-16',
    }, {
      name: 'Jack',
      sex: '男',
      age: '14',
      time: '2020-11-16',
    }, {
      name: 'Tom',
      sex: '猫',
      age: '15',
      time: '2020-11-16',
    }, {
      name: 'Jerry',
      sex: '老鼠',
      age: '14',
      time: '2020-11-16',
    }, {
      name: '张三',
      sex: '男',
      age: '10',
      time: '2020-11-16',
    }, {
      name: '李四',
      sex: '男',
      age: '11',
      time: '2020-11-16',
    }]
  },
  methods: {
    headerCellContextMenuEvent ({ type, column, columnIndex, $event, }) {
      console.log(type, column, columnIndex, $event)
      this.$refs.xTable.setCurrentColumn(column)
    },
    footerCellContextMenuEvent ({ type, column, columnIndex, $event, }) {
      console.log(type, column, columnIndex, $event)
    },
    cellContextMenuEvent ({ type, row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event, }) {
      console.log(type, row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event)
      this.$refs.xTable.setCurrentRow(row)
    },
    visibleMethod ({ options, column, }) {
      // 示例：只有 name 列允许操作，清除按钮只能在 age 才显示
      // 显示之前处理按钮的操作权限
      const isDisabled = !column || column.property !== 'name'
      const isVisible = column && column.property === 'age'
      options.forEach(list => {
        list.forEach(item => {
          if (['copy', 'remove'].includes(item.code)) {
            item.disabled = isDisabled
          }
          if (['details'].includes(item.code)) {
            item.visible = column.property === 'name'
          } else if (['clear', 'filter'].includes(item.code)) {
            item.visible = isVisible
          }
        })
      })
      return true
    },
    contextMenuClickEvent ({ menu, type, row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event, }) {
      console.log('menuClick', menu, type, row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event)
      switch (menu.code) {
        case 'copy':
          // 示例
          if (row && column) {
            if (copyText(row[column.property])) {
              message.success('已复制到剪贴板！')
            }
          }
          break
        default:
          message.info(`点击了 "${menu.name}"`)
      }
    },
    footerMethod ({ columns, data, }) {
      return [
        columns.map((column, columnIndex) => {
          if (columnIndex === 0) {
            return '平均'
          }
          if (['age', 'rate'].includes(column.property)) {
            return parseInt(mean(data, column.property))
          }
          return null
        })
      ]
    },
  },
}
</script>

```
