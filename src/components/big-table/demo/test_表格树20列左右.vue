<template>
  <ta-big-table
    ref="xTree"
    resizable
    show-overflow
    :tree-config="{children: 'children', lazy: true, hasChild: 'hasChild', loadMethod: loadChildrenMethod, accordion: true}"
    :edit-config="{trigger: 'click', mode: 'row'}"
    :data="tableData"
    :checkbox-config="{labelField: 'id'}"
  >
    <ta-big-table-column type="checkbox" title="ID" width="500" tree-node fixed="left" />
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
</template>
<script lang="jsx">
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
  const tableData = []
  for (let i = 0; i < 100; i++) {
    tableData.push({
      id: i.toString(),
      name: '前端入门到放弃' + i,
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
      hasChild: true,
    })
  }
  export default {
    data () {
      return {
        hobbyList,
        addressList,
        tableData,
      }
    },
    methods: {
      loadChildrenMethod ({ row, }) {
        let result = []
        for (let i = 0; i < 100; i++) {
          result.push({
            ...row,
            id: row.id + '_' + i,
            name: '前端入门到放弃' + row.id + '_' + i,
            children: [],
            _XID: '',
          })
        }
        return Promise.resolve(result)
      },
    },
  }
</script>
