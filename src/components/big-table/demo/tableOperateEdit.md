
<cn>
#### 行编辑
- ta-big-table使用`table-operate`组件控制行编辑
- ta-big-table必须设置`keep-source`属性
- ta-big-table的`edit-config`配置必须配置为(自定义触发,模式行编辑,自动关闭编辑false`{trigger: 'manual', mode: 'row',autoClear:false}`) 
</cn>

<us>
#### row Editor
</us>

```html
<template>
  <div>
    <ta-big-table
      ref="plTable"
      :data="tableData"
      height="300px"
      use-virtual
      :edit-rules="validRules"
      show-body-overflow="title"
      show-header-overflow="title"
      keep-source
      :edit-config="{trigger: 'manual', mode: 'row',autoClear:false}"
    >
      <ta-big-table-column type="index" width="100" fixed />
      <ta-big-table-column
        :resizable="true"
        :show-overflow-tooltip="true"
        field="name"
        title="姓名"
        :edit-render="{name: '$input'}"
      />
      <ta-big-table-column
        :resizable="true"
        :show-overflow-tooltip="true"
        field="age"
        title="年龄"
        :edit-render="{name: '$input-number'}"
      />
      <ta-big-table-column
        fixed="right"
        field="operate"
        title="操作"
        width="400"
        align="center"
      >
        <span slot-scope="rowInfo">
          <ta-table-operate overflow-tooltip :operate-menu="operateMenu" :row-info="rowInfo" />
        </span>
      </ta-big-table-column>
    </ta-big-table>
  </div>
</template>
<script>
export default {
  data () {
    const col = ['id', 'date', 'name', 'address', 'age']
    return {
      validRules: {
        name: [
          { required: true, message: '姓名必须填写', }
        ],
      },
      tableData: Array.from({ length: 5, }, (_, idx) => ({
        id: idx + 1,
        name: '张三' + idx,
        age: idx + 1,
      })),
      operateMenu: [
        {
          name: '编辑',
          icon: false,
          type: 'edit',
          // 自定义保存和取消按钮样式
          editConfig: {
            // saveConfig: {
            //   name: '保存',
            // },
            cancelConfig: {
              name: '取消',
              icon: false,
            },
          },
          // 保存前使用,返回false表示不保存,主要用于验证
          beforeSave: (newRow, oldRow) => {
            // 可以编辑的行手动调用验证
            return this.$refs.plTable.validate(newRow).then(() => {
              return true
            }).catch((err) => {
              return false
            })
            // 或者你自己的逻辑...
          },
          // 保存后调用
          onSave: (record) => {
            // 这里可以调用提交submit....

          },
          // 取消时调用
          onCancel: (record) => {
            // ....

          },
        },
        {
          name: '删除',
          icon: false,
          type: 'confirm',
          confirmTitle: '确认删除该信息？',
          onOk: (record, index) => {
            this.tableData.splice(index, 1)
            message.info('删除信息成功')
          },
        }

      ],
    }
  },
}
</script>

```
