<cn>
#### 原生编辑编辑
- ta-big-table提供一套`input、textarea、select`原生html组件的编辑
- ta-big-table配置edit-config开启编辑
- ta-big-table在列标签上使用edit-render的name配置使用什么控件，可选的有input、textarea、select,使用mode配置行编辑或者表格编辑,使用showStatus和big-table的keep-source属性控制是否显示修改状态
- ta-big-table通过keep-source属性开启时保存原数据，可以通过ref调用big-table的revertData方法还原数据
</cn>

<us>
#### edit
edit
</us>

```html
<template>
  <div>
    <p style="margin-bottom: 20px">单元格编辑</p>
    <div style="margin-bottom: 20px">
      <ta-button @click="insertEvent">新增</ta-button>
      <ta-button @click="getInsertEvent">获取新增</ta-button>
      <ta-button @click="getSelectEvent">获取选中</ta-button>
      <ta-button @click="$refs.xTable.removeCheckboxRow()">删除选中</ta-button>
      <ta-button @click="getRemoveEvent">获取删除</ta-button>
      <ta-button @click="getUpdateEvent">获取修改</ta-button>
      <ta-button @click="validEvent">校验</ta-button>
      <ta-button @click="fullValidEvent">完整校验</ta-button>
      <ta-button @click="validAllEvent">全量校验</ta-button>
      <ta-button @click="selectValidEvent">选中校验</ta-button>
      <ta-popconfirm title="确定还原数据吗?" ok-text="确定" cancel-text="取消" @confirm="revertEvent">
        <ta-button>还原数据</ta-button>
      </ta-popconfirm>
    </div>
    <ta-big-table
      ref="xTable"
      border
      resizable
      keep-source
      show-overflow
      :data="tableData"
      :edit-rules="validRules"
      :edit-config="{trigger: 'click', mode: 'cell', showStatus: true}"
    >
      <ta-big-table-column type="checkbox" width="60" />
      <ta-big-table-column type="seq" width="60" />
      <ta-big-table-column field="name" title="Name" :edit-render="{name: 'input'}" />
      <ta-big-table-column field="role" title="Role" :edit-render="{name: 'input'}" />
      <ta-big-table-column field="sex" title="Sex" :edit-render="{name: 'select', options: sexList}" />
      <ta-big-table-column field="age" title="Age" :edit-render="{name: 'input'}" />
    </ta-big-table>
    <p style="margin-bottom: 20px">
      行编辑
    </p>
    <ta-big-table
      border
      resizable
      keep-source
      show-overflow
      :data="tableData"
      :edit-rules="validRules"
      :edit-config="{trigger: 'click', mode: 'row', showStatus: true}"
    >
      <ta-big-table-column type="seq" width="60" />
      <ta-big-table-column field="name" title="Name" :edit-render="{name: 'input'}" />
      <ta-big-table-column field="role" title="Role" :edit-render="{name: 'input'}" />
      <ta-big-table-column field="sex" title="Sex" :edit-render="{name: 'select', options: sexList}" />
      <ta-big-table-column field="age" title="Age" :edit-render="{name: 'input'}" />
    </ta-big-table>
  </div>
</template>

<script>
export default {
  data () {
    const nameValid = ({ cellValue, }) => {
      if (cellValue && (cellValue.length < 3 || cellValue.length > 50)) {
        return new Error('名称长度在 3 到 50 个字符之间')
      }
    }
    const roleValid = ({ cellValue, }) => {
      if (cellValue && !['前端', '后端', '设计师', '项目经理', '测试'].includes(cellValue)) {
        return new Error('角色输入不正确')
      }
    }
    return {
      tableData: [
        { id: 10001, name: 'Test1', role: '前端', sex: '0', age: 40, },
        { id: 10002, name: 'Test2', role: '后端', sex: '1', age: 222, },
        { id: 10003, name: 'Test3', role: '后端', sex: '0', age: 200, },
        { id: 10004, name: 'Test4', role: '设计师', sex: '1', age: 30, },
        { id: 10005, name: 'Test5', role: '后端', sex: '0', age: 20, },
        { id: 10006, name: 'Test6', role: '项目经理', sex: '1', age: 10, },
        { id: 10007, name: 'Test7', role: '测试', sex: '0', age: 5, },
        { id: 10008, name: 'Test8', role: '前端', sex: '1', age: 2, }
      ],
      sexList: [
        { label: '请选择', value: '0', },
        { label: '男', value: '1', },
        { label: '女', value: '2', }
      ],
      validRules: {
        name: [
          { required: true, message: '姓名必须填', },
          { validator: nameValid, }
        ],
        role: [
          { validator: roleValid, }
        ],
        sex: [
          { required: true, message: '性别必须填写', },
          { pattern: /^[1,2]{1}$/, message: '格式不正确', }
        ],
        age: [
          { pattern: '^[0-9]{0,3}$', message: '格式不正确', }
        ],
      },
    }
  },
  methods: {
    insertEvent () {
      this.$refs.xTable.insert([{name: '新添加的行', role: '测试', sex: '1', age: 20, }]).then((newRow) => {
        this.$refs.xTable.validate(newRow.rows).catch(errMap => {
          if (errMap) {
            message.error('新添加的行校验不通过！(可自定义是否校验)')
          }
        })
      })
    },
    getInsertEvent () {
      let insertRecords = this.$refs.xTable.getInsertRecords()
      message.info(insertRecords.length)
    },
    getSelectEvent () {
      let selectRecords = this.$refs.xTable.getCheckboxRecords()
      message.info(selectRecords.length)
    },
    getRemoveEvent () {
      let removeRecords = this.$refs.xTable.getRemoveRecords()
      message.info(removeRecords.length)
    },
    getUpdateEvent () {
      let updateRecords = this.$refs.xTable.getUpdateRecords()
      message.info(updateRecords.length)
    },
    validEvent () {
      // 不指定数据，则默认只校验临时变动的数据，例如新增或修改，当某一列校验失败后会停止校验
      this.$refs.xTable.validate().then(() => {
        message.success('校验成功！')
      }).catch(errMap => {
        errMap && message.error('校验不通过！')
        console.log(errMap)
      })
    },
    fullValidEvent () {
      // 不指定数据，则默认只校验临时变动的数据，例如新增或修改，当某一列校验失败后不会停止校验
      this.$refs.xTable.fullValidate().then(() => {
        message.success('校验成功！')
      }).catch(errMap => {
        if (errMap) {
          let msgList = []
          Object.values(errMap).forEach(errList => {
            errList.forEach(params => {
              let { rowIndex, column, rules, } = params
              rules.forEach(rule => {
                msgList.push(`第 ${rowIndex} 行 ${column.title} 校验错误：${rule.message}`)
              })
            })
          })
          message.error(msgList.join())
        }
      })
    },
    validAllEvent () {
      // 传入true完整校验整个表格中所有数据
      this.$refs.xTable.validate(true).then(() => {
        message.success('校验成功！')
      }).catch(errMap => {
        errMap && message.error('校验不通过！')
      })
    },
    selectValidEvent () {
      // 传入选中行，校验选中行
      let selectRecords = this.$refs.xTable.getCheckboxRecords()
      if (selectRecords.length > 0) {
        this.$refs.xTable.validate(selectRecords).then(() => {
          message.success('校验成功！')
        }).catch(errMap => {
          errMap && message.error('校验不通过！')
        })
      } else {
        message.warning('未选中数据！')
      }
    },
    revertEvent () {
      this.$refs.xTable.revertData()
    },
  },
}
</script>

```
