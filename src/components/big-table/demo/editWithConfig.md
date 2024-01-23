<cn>
#### 表格编辑
- ta-big-table的内置编辑组件为ta404UI组件库中的组件,所以编辑组件的属性可通过本文档查阅,并可通过edit-render传入例如:
```
<ta-big-table-column :edit-render="{name: '$input', props: {autoFocus: true, },style:{},class:'myclass'}" />
```
- 如果需要更复杂的表格编辑可使用自定义编辑表格，需要使用插槽
- ta-big-table可以在列标签内传入默认插槽或者在列的edit-render属性中传入一个名为renderCell的函数进行自定义渲染默认值
- ta-big-table行编辑时需要自行指定哪一列是自动focus的，例如本例的Age列，单元格编辑会自动focus当前编辑的单元格
- ta-big-table的日期编辑需要设置format和formatValue
- ta-big-table编辑有弹出框的容器的默认是弹出在body的，如果需要弹出在表格内部，需要自定义getPopupContainer和设置 edit-render.dropDownInBody 为false
</cn>

<us>
#### complex edit
complex edit
</us>

```html
<template>
  <div>
    <ta-big-table
      ref="xTable"
      border
      height="400px"
      resizable
      keep-source
      show-overflow
      :data="tableData"
      :edit-rules="validRules"
      :edit-config="{trigger: 'click', mode: 'row',showStatus: true}"
      @edit-closed="editClosed"
    >
      <ta-big-table-column type="checkbox" width="60" fixed="left" />
      <ta-big-table-column type="seq" width="60" fixed="left" />
      <ta-big-table-column field="name" title="Name" width="150" :edit-render="{name: '$input', props: {autoFocus: true, }}" />
      <ta-big-table-column field="age" title="Age" width="150" :edit-render="{name: '$input-number', renderCell: renderDefaultAge, style: {color: 'red', width: '100%'}}" />
      <ta-big-table-column field="sex" title="Sex" width="150" collection-type="SEX" :edit-render="{name: '$select'}" />
      <ta-big-table-column field="hobby" width="220px" title="多选下拉" :edit-render="{name: '$select', props: {maxTagCount: 2,mode: 'multiple',options: hobbyList}}" />
      <ta-big-table-column field="date" title="Date" width="150" :edit-render="{name: '$date-picker', props: {format: 'YYYY-MM-DD'}}" />
      <ta-big-table-column field="time" title="Time" width="150" :edit-render="{name: '$time-picker', props: {format: 'HH:mm:ss'}}" />
      <ta-big-table-column field="month" title="Month" width="150" :edit-render="{name: '$month-picker', props: {format: 'YYYY-MM'}}" />
      <ta-big-table-column field="range" title="Range" width="250" :edit-render="{name: '$range-picker', props: {format: 'YYYY-MM-DD'}}" />
      <ta-big-table-column field="week" title="Week" width="150" :edit-render="{name: '$week-picker', props: {format: 'YYYY年第ww周'}}" />
      <ta-big-table-column field="quarter" title="Quarter" width="150" :edit-render="{name: '$quarter-picker', props: {format: 'YYYY年Q季度'}}" />
      <ta-big-table-column field="year" title="Year" width="150" :edit-render="{name: '$year-picker', props: {format: 'YYYY年'}}" />
      <ta-big-table-column field="rate" title="Rate" width="200" :edit-render="{name: '$rate'}" />
      <ta-big-table-column field="switch" title="Switch" width="150" :edit-render="{name: '$switch', trueText: '有效', falseText: '无效'}" />
      <ta-big-table-column field="checkbox" title="Checkbox" width="150" :edit-render="{name: '$checkbox'}" />
      <ta-big-table-column field="radio" title="Radio" width="150" :edit-render="{name: '$radio' , props: {cancelChecked: true}}" />
      <ta-big-table-column field="radioGroup" title="RadioGroup" width="320" :edit-render="{name: '$radio-group', props: {options: hobbyList}}" />
      <ta-big-table-column field="checkboxGroup" title="CheckboxGroup" width="300" :edit-render="{name: '$checkbox-group', props: {options: hobbyList}}" />
      <ta-big-table-column field="cascader" title="Cascader" width="300" :edit-render="{name: '$cascader', props: {options: addressList}}" />
      <ta-big-table-column field="treeSelect" title="TreeSelect" width="300" :edit-render="{name: '$tree-select', showPath: true, props: {treeData: addressList}}" />
      <ta-big-table-column field="addresses" title="TreeSelect多选" width="300" :edit-render="{name: '$tree-select', props: {multiple: true, maxTagCount: 2, treeData: addressList}}" />
    </ta-big-table>
  </div>
</template>

<script >
const hobbyList = [{label: '足球', value: 0, }, {label: '篮球', value: 1, }, {label: '排球', value: 2, }, {label: '乒乓球', value: 3, }]
const addressList = [{
  value: 'zhejiang',
  label: '浙江',
  children: [{
    value: 'hangzhou',
    label: '杭州',
    children: [{
      value: 'xihu',
      label: '西湖',
    }],
  }],
}, {
  value: 'jiangsu',
  label: '江苏',
  children: [{
    value: 'nanjing',
    label: '南京',
    children: [{
      value: 'zhonghuamen',
      label: '中华门',
    }],
  }],
}]

const data = []
for (let i = 0; i < 6; i++) {
  data.push({
    key: i.toString(),
    name: `Name ${i}`,
    age: i,
    sex: `${i % 3}`,
    hobby: [i % 4],
    date: '2019-05-10',
    month: '2019-05-10',
    range: ['2019-05-10', '2019-05-19'],
    week: '2019-05-10',
    rate: i % 6,
    switch: Boolean(i % 2),
    checkbox: Boolean(i % 2),
    radio: Boolean(i % 2),
    address: ['jiangsu', 'nanjing', 'zhonghuamen'],
    treeSelect: 'nanjing',
    addresses: ['jiangsu', 'nanjing', 'zhonghuamen'],
    cascader: ['jiangsu', 'nanjing', 'zhonghuamen'],
    quarter: '2019-05-10',
    year: '2019-05-10',
    radioGroup: i % 4,
    checkboxGroup: [i % 4],
    time: '2019-05-10 09:50:50',
  })
}
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
      tableData: data,
      hobbyList,
      addressList,
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
      editClosed ({ row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, }) {
          this.$refs.xTable.validate([row]).then(() => {
              console.log({ row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, })
          }).catch(() => {
              this.$refs.xTable.revertData([row], column.property)
          })
      },
    renderDefaultAge(h, renderOpts, {cellValue, }){
      return cellValue + ' 岁'
    },
  },
}
</script>

```
