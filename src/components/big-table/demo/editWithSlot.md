<cn>
#### 自定义编辑
- ta-big-table-column使用edit插槽进行自定义
- 组件必须使用v-model进行双向绑定
- 组件必须添加width:100%的样式
- 如果需要进行校验，则需要监听change事件，封装一个通用的更新表格数据的方法，调用即可
</cn>

<us>
#### custom edit
custom edit
</us>

```html
<template>
  <div>
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
      height="300px"
      resizable
      keep-source
      show-overflow
      :data="tableData"
      :edit-rules="validRules"
      :edit-config="{trigger: 'click', mode: 'cell',showStatus: true}"
    >
      <ta-big-table-column type="checkbox" width="60" />
      <ta-big-table-column type="seq" width="60" />
      <ta-big-table-column field="name" title="Name" :edit-render="{}">
        <template #edit="{row, column}">
          <ta-input v-model="row.name" auto-focus style="width: 100%" @change="(e) => handleChange(e.target.value, row, column)" />
        </template>
      </ta-big-table-column>
      <ta-big-table-column field="sex" title="Sex" collection-type="SEX" :edit-render="{}">
        <template #edit="{row, column}">
          <ta-select v-model="row.sex" auto-focus style="width: 100%" :options="sexList" :get-popup-container="setPopupContainer" @change="(value) => handleChange(value, row, column)"/>
        </template>
      </ta-big-table-column>
      <ta-big-table-column field="sex2" width="220px" title="多选下拉" :formatter="formatter" :edit-render="{}">
        <template #edit="{row, column}">
          <ta-select v-model="row.sex2" :maxTagCount="2" auto-focus style="width: 100%" mode="multiple" :options="sexList" :get-popup-container="setPopupContainer" @change="(value) => handleChange(value, row, column)"/>
        </template>
      </ta-big-table-column>
      <ta-big-table-column field="num1" title="Amount" :edit-render="{}">
        <template #edit="{row, column}">
          <ta-input-number v-model="row.num1" auto-focus style="width: 100%" :precision="2" @change="(value) => handleChange(value, row, column)"/>
        </template>
      </ta-big-table-column>
      <ta-big-table-column field="date12" title="Date" :edit-render="{}">
        <template #edit="{row, column}">
          <ta-date-picker v-model="row.date12" auto-focus style="width: 100%" value-format="YYYY-MM-DD" format="YYYY-MM-DD" :get-calendar-container="setPopupContainer" @change="(value) => handleChange(value, row, column)"/>
        </template>
      </ta-big-table-column>
      <ta-big-table-column field="date13" title="year" :formatter="formatYearDate" :edit-render="{}">
        <template #edit="{row, column}">
          <ta-year-picker v-model="row.date13" auto-focus style="width: 100%" value-format="YYYY-MM-DD" format="YYYY年" :get-calendar-container="setPopupContainer" @change="(value) => handleChange(value, row, column)"/>
        </template>
      </ta-big-table-column>
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
        { id: 10001, name: 'Test1', nickname: 'T1', role: '前端', sex: '0', sex2: ['0'], num1: 40, age: 28, address: 'Shenzhen', date12: '', date13: '', },
        { id: 10002, name: 'Test2', nickname: 'T2', role: '后端', sex: '1', sex2: ['0', '1'], num1: 200, age: 22, address: 'Guangzhou', date12: '', date13: '2020-08-20', },
        { id: 10003, name: 'Test3', nickname: 'T3', role: '设计师', sex: '0', sex2: ['1'], num1: 200, age: 32, address: 'Shanghai', date12: '2020-09-10', date13: '', },
        { id: 10004, name: 'Test4', nickname: 'T4', role: '项目经理', sex: '1', sex2: ['1'], num1: 30, age: 23, address: 'Shenzhen', date12: '', date13: '2020-12-04', },
        { id: 10005, name: 'Test5', nickname: 'T5', role: '测试', sex: '0', sex2: ['1', '0'], num1: 20, age: 30, address: 'Shanghai', date12: '2020-09-20', date13: '', },
        { id: 10006, name: 'Test6', nickname: 'T6', role: '设计师', sex: '1', sex2: ['0'], num1: 10, age: 21, address: 'Shenzhen', date12: '', date13: '', },
        { id: 10007, name: 'Test7', nickname: 'T7', role: '设计师', sex: '0', sex2: ['0'], num1: 5, age: 29, address: 'Shenzhen', date12: '2020-01-02', date13: '2020-09-20', },
        { id: 10008, name: 'Test8', nickname: 'T8', role: '前端', sex: '1', sex2: ['0'], num1: 2, age: 35, address: 'Shenzhen', date12: '', date13: '', }
      ],
      sexList: [
        { label: '无', value: '0', },
        { label: '男', value: '1', },
        { label: '女', value: '2', }
      ],
      validRules: {
        name: [
          { required: true, message: '姓名必须填写', },
          { validator: nameValid, }
        ],
        role: [
          { validator: roleValid, }
        ],
        sex: [
          { required: true, message: '性别必须填写', },
          { pattern: /^[1,2]{1}$/, message: '格式不正确', }
        ],
        sex2: [
          { required: true, message: '性别必须填写', }
        ],
        num1: [
          { required: true, message: 'number必须填写', }
        ],
        age: [
          { pattern: '^[0-9]{0,3}$', message: '格式不正确', }
        ],
        date12: [
          { required: true, message: '日期必须填写', }
        ],
        date13: [
          { required: true, message: '日期必须填写', }
        ],
      },
    }
  },
  methods: {
    formatter({cellValue, }){
      return cellValue.map(item => this.sexList.find(innerItem => innerItem.value === item).label).join(',')
    },
    formatYearDate({cellValue, }){
      return cellValue && cellValue !== '' && cellValue.slice(0, 4) + '年'
    },
    setPopupContainer(trigger){
      return trigger.parentNode
    },
    handleChange(value, row, column){
      this.$refs.xTable.updateStatus({row, column, }, value)
    },
    insertEvent () {
      this.$refs.xTable.insert([{ id: 999, name: '新增加的行', nickname: 'T1', role: '前端', sex: '0', sex2: ['0'], num1: 40, age: 28, address: 'Shenzhen', date12: '', date13: '', }]).then((newRow) => {
        this.$refs.xTable.validate(newRow).catch(errMap => {
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
