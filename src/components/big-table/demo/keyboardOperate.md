<cn>
#### 键盘导航
- ta-big-table行通过`highlight-current-row` + `:keyboard-config="{isArrow: true}"` 开启移动行键盘导航
- ta-big-table单元格通过`:mouse-config="{selected: true}"` + :keyboard-config="{isArrow: true, isDel: true, isEnter: true, isTab: true, isEdit: true}" 配置单元格选中+键盘操作
</cn>

<us>
#### keyboard operate
keyboard operate
</us>

```html
<template>
  <div>
    <p style="margin-bottom: 20px">
      键盘移动高亮行：
    </p>
    <ta-big-table
      ref="xTable1"
      border
      resizable
      show-overflow
      highlight-current-row
      keep-source
      height="300"
      :loading="loading"
      :keyboard-config="{isArrow: true}"
      @current-change="handleTableCurrentChange"
    >
      <ta-big-table-column type="checkbox" width="60" />
      <ta-big-table-column type="seq" width="100" />
      <ta-big-table-column field="name" title="Name" sortable width="200" :edit-render="{name: 'input'}" />
      <ta-big-table-column field="age" title="Age" width="200" :edit-render="{name: 'input'}" />
      <ta-big-table-column field="sex" title="Sex" width="200" :edit-render="{name: 'input'}" />
      <ta-big-table-column field="rate" title="Rate" width="200" />
      <ta-big-table-column field="region" title="Region" width="200" />
      <ta-big-table-column field="time" title="Time" width="200" />
      <ta-big-table-column field="address" title="Address" width="300" show-overflow />
      <ta-big-table-column field="updateTime" title="UpdateTime" width="200" />
      <ta-big-table-column field="createTime" title="CreateTime" width="200" />
    </ta-big-table>

    <p style="margin: 20px 0">
      键盘导航：
    </p>
    <ta-big-table
      ref="xTable2"
      border
      resizable
      show-overflow
      keep-source
      height="300"
      :loading="loading"
      :edit-rules="validRules"
      :mouse-config="{selected: true}"
      :edit-config="{trigger: 'dblclick', mode: 'cell', showStatus: true}"
      :keyboard-config="{isArrow: true, isDel: true, isEnter: true, isTab: true, isEdit: true}"
      :checkbox-config="{checkField: 'checked'}"
      @cell-selected="handleCellSelect"
    >
      <ta-big-table-column type="checkbox" width="60" />
      <ta-big-table-column type="seq" width="100" />
      <ta-big-table-column field="name" title="Name" sortable width="200" :edit-render="{name: '$input'}" />
      <ta-big-table-column field="age" title="Age" width="200" :edit-render="{name: '$input'}" />
      <ta-big-table-column field="sex" title="Sex" width="200" :edit-render="{name: '$input'}" />
      <ta-big-table-column field="rate" title="Rate" width="200" />
      <ta-big-table-column field="region" title="Region" width="200" />
      <ta-big-table-column field="time" title="Time" width="200" />
      <ta-big-table-column field="address" title="Address" width="300" show-overflow />
      <ta-big-table-column field="updateTime" title="UpdateTime" width="200" />
      <ta-big-table-column field="createTime" title="CreateTime" width="200" />
    </ta-big-table>
  </div>
</template>

<script>
const data = Array.from({length: 5000, }).map((item, index) => ({
  name: 'test' + index,
  sex: index,
  age: index,
  address: index,
  rate: 3,
  region: 'testtest',
  time: '2020-11-25',
  updateTime: '2020-11-26',
  createTime: '2020-11-27',
  checked: false,
}))
export default {
  data () {
    return {
      loading: false,
      validRules: {
        name: [
          { required: true, message: 'Name必填', },
          { min: 3, max: 50, message: '名称长度在 3 到 50 个字符', }
        ],
        sex: [
          { required: true, message: '性别必须填写', }
        ],
      },
    }
  },
  created () {
    this.findList()
  },
  methods: {
    findList () {
      this.loading = true
      return new Promise(resolve => {
        setTimeout(() => {
          // 阻断 vue 对大数组的监听，避免 vue 绑定大数据造成短暂的卡顿
          if (this.$refs.xTable1) {
            this.$refs.xTable1.loadData(data)
          }
          if (this.$refs.xTable2) {
            this.$refs.xTable2.loadData(data)
          }
          resolve()
          this.loading = false
        }, 300)
      })
    },
    handleTableCurrentChange({ row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event, }) {
      // 使用鼠标点击时会传递column相关参数，使用键盘方向键导航则不传递column相关参数
      console.log(row, column)
    },
    handleCellSelect({ row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, }){
      console.log(row, column)
    },
  },
}
</script>
```
