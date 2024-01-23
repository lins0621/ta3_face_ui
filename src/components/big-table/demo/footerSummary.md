<cn>
#### 表尾合计行
ta-big-table使用show-footer=true开启表尾，使用footer-method属性传递计算表尾数据信息的方法，使用footer-cell-class-name传递计算表尾数据css类的方法
</cn>

<us>
#### footer summary
footer summary
</us>

```html
<template>
  <div>
    <div style="margin-bottom: 20px">
      <ta-button @click="insertEvent">
        新增
      </ta-button>
      <ta-button @click="removeEvent">
        删除
      </ta-button>
      <ta-button @click="saveEvent">
        保存
      </ta-button>
    </div>
    <ta-big-table
      ref="xTable"
      border
      height="400px"
      show-footer
      resizable
      keep-source
      show-overflow
      :data="tableData"
      :footer-method="footerMethod"
      :footer-cell-class-name="footerCellClassName"
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
          <ta-select v-model="row.sex" auto-focus style="width: 100%" collection-type="SEX" :get-popup-container="setPopupContainer" @change="(value) => handleChange(value, row, column)" />
        </template>
      </ta-big-table-column>
      <ta-big-table-column field="age" title="Age" :edit-render="{}">
        <template #edit="{row, column}">
          <ta-input-number v-model="row.age" auto-focus style="width: 100%" @change="(value) => handleChange(value, row, column)" />
        </template>
      </ta-big-table-column>
      <ta-big-table-column field="num1" title="Amount" :edit-render="{}">
        <template #edit="{row, column}">
          <ta-input-number v-model="row.num1" auto-focus style="width: 100%" :precision="2" @change="(value) => handleChange(value, row, column)" />
        </template>
      </ta-big-table-column>
    </ta-big-table>
  </div>
</template>

<script >
import { mean, sum, } from '@yh/ta-utils'
export default {
  data () {
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
    }
  },
  methods: {
    setPopupContainer(trigger){
      return trigger.parentNode
    },
    handleChange(value, row, column){
      this.$refs.xTable.updateStatus({row, column, }, value)
    },
    footerCellClassName ({ $rowIndex, column, columnIndex, }) {
      if (columnIndex === 0) {
        if ($rowIndex === 0) {
          return 'col-blue'
        } else {
          return 'col-red'
        }
      }
    },
    footerMethod ({ columns, data, }) {
      return [
        columns.map((column, columnIndex) => {
          if (columnIndex === 0) {
            return '平均'
          }
          if (['age'].includes(column.property)) {
            return parseInt(mean(data, column.property))
          }
          if (['num1'].includes(column.property)) {
            return parseFloat(mean(data, column.property)).toFixed(2)
          }
          return null
        }),
        columns.map((column, columnIndex) => {
          if (columnIndex === 0) {
            return '和值'
          }
          if (['age'].includes(column.property)) {
            return sum(data, column.property)
          }
          if (['num1'].includes(column.property)) {
            return sum(data, column.property).toFixed(2)
          }
          return null
        })
      ]
    },
    insertEvent () {
      let record = {
        name: 'New name',
        age: 18,
      }
      this.$refs.xTable.insert(record).then(({ row, }) => this.$refs.xTable.setActiveCell(row, 'age'))
    },
    removeEvent () {
      this.$refs.xTable.removeCheckboxRow()
    },
    saveEvent () {
      const { insertRecords, removeRecords, updateRecords, } = this.$refs.xTable.getRecordset()
      message.info(`insertRecords=${insertRecords.length} removeRecords=${removeRecords.length} updateRecords=${updateRecords.length}`)
    },
  },
}
</script>

<style>
.col-blue{
  background-color: #2db7f5;
  color: white;
}
.col-red{
  background-color: #ff0000;
  color: white;
}
</style>

```
