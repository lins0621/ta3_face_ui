
<cn>
#### 树编辑
ta-big-table可以通过一些API对树结构进行插入数据修改数据等
</cn>

<us>
#### Tree Edit 
You can set the operation column and customize the editing status of the control table by setActiveRow, clearActived and other methods.
</us>

```html
<template>
  <div>
    <ta-big-table
      ref="xTable"
      max-height="600"
      row-id="id"
      :data="tableData"
      :tree-config="{expandAll: true}"
    >
      <ta-big-table-column field="name" title="名称" tree-node />
      <ta-big-table-column field="size" title="大小" width="140" />
      <ta-big-table-column field="type" title="类型" width="140" />
      <ta-big-table-column field="date" title="修改日期" width="260" />
      <ta-big-table-column
        fixed="right"
        field="operate"
        title="操作"
      >
        <span slot-scope="rowInfo">
          <ta-table-operate :operate-menu="operateMenu" :row-info="rowInfo" />
        </span>
      </ta-big-table-column>
    </ta-big-table>
    <ta-modal
      v-model="visible"
      :title="editType === 'edit' ? '编辑' : '新增下级'"
      height="300px"
    >
      <ta-form :auto-form-create="createForm">
        <ta-form-item v-if="editType === 'addChild'" disabled label="父数据名称" field-decorator-id="parentName">
          <ta-input />
        </ta-form-item>
        <ta-form-item label="名称" field-decorator-id="name">
          <ta-input />
        </ta-form-item>
        <ta-form-item label="大小" field-decorator-id="size">
          <ta-input />
        </ta-form-item>
        <ta-form-item label="类型" field-decorator-id="type">
          <ta-input />
        </ta-form-item>
      </ta-form>
      <template slot="footer">
        <ta-button key="back" @click="cancel">
          取消
        </ta-button>
        <ta-button v-if="editType === 'edit'" key="submit" type="primary" @click="saveEdit">
          保存编辑
        </ta-button>
        <ta-button v-else key="submit" type="primary" @click="addChild">
          新增
        </ta-button>
      </template>
    </ta-modal>
  </div>
</template>
<script>
import { uuidV4, } from '@yh/ta-utils'

export default {
  data () {
    return {
      editType: 'edit',
      visible: false,
      count: 0,
      form: null,
      clickRowData: null,
      tableData: window.mockTreeData,
      operateMenu: [
        {
          name: '添加下级',
          icon: 'plus',
          onClick: (record, index) => {
            this.editType = 'addChild'
            this.visible = true
            this.clickRowData = record
            this.$nextTick(() => {
              this.form.resetFields()
              this.form.setFieldsValue({
                parentName: record.name,
              })
            })
          },
        }
      ],
    }
  },
  methods: {
    createForm (form) {
      this.form = form
    },
    saveTableData () {
      // 调用loadData方法，将临时数据变成原始数据
      const fullData = this.$refs.xTable.getTableData().fullData
      this.$refs.xTable.loadData(fullData)
      // 模拟从后端加载数据
      setTimeout(() => {
        this.$refs.xTable.loadData([...fullData, {
          id: 'fasdfasdf',

          name: 'ta-big-table 入坑系列 fadfadfasfd.png',
          size: '66k',
          type: 'png',
          date: '2019-08-23',
          childCols: [],
          childData: [],
          checked: false,
          indeterminate: false,
        }])
      }, 1 * 1000)
    },
    cancel () {
      this.visible = false
    },
    addChild () {
      const formData = this.form.getFieldsValue()
      const data = { ...formData, ...{ id: uuidV4(), parentId: this.clickRowData.id, }, }
      console.log(data)
      this.$refs.xTable.insert(data)
      this.saveTableData()
      this.visible = false
      this.clickRowData = null
    },
    saveEdit () {
      const formData = this.form.getFieldsValue()
      const data = { ...this.clickRowData, ...formData, }
      this.$refs.xTable.reloadTreeRow(this.clickRowData, data)
      this.visible = false
      this.clickRowData = null
    },
  },
}
</script>

```
