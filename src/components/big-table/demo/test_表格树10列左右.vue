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
    <ta-big-table-column type="checkbox" title="ID" width="500" tree-node />
    <ta-big-table-column field="name" title="Name" width="200" :edit-render="{name: '$input', props: {autoFocus: true, }}" />
    <ta-big-table-column field="role" title="Role" width="200" :edit-render="{name: '$input'}" />
    <ta-big-table-column field="sex" title="Sex" width="200" :edit-render="{name: '$select'}" collection-type="SEX" />
    <ta-big-table-column field="age" title="Age" width="200" :edit-render="{name: '$input-number'}" />
    <ta-big-table-column field="cascader" title="Cascader" width="200" :edit-render="{name: '$cascader', props: {options: addressList}}" />
    <ta-big-table-column field="quarter" title="Quarter" width="200" :edit-render="{name: '$quarter-picker', props: {format: 'YYYY年Q季度'}}" />
    <ta-big-table-column field="hobby" title="多选下拉" width="200" :edit-render="{name: '$select', props: {maxTagCount: 2,mode: 'multiple',options: hobbyList}}" />
    <ta-big-table-column field="switch" title="Switch" width="200" :edit-render="{name: '$switch', trueText: '有效', falseText: '无效'}" />
    <ta-big-table-column field="checkbox" title="Checkbox" width="200" :edit-render="{name: '$checkbox'}" />
    <ta-big-table-column field="treeSelect" title="TreeSelect" width="200" :edit-render="{name: '$tree-select', showPath: true, props: {treeData: addressList}}" />
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
  for (let i = 0; i < 200; i++) {
    tableData.push({
      id: i.toString(),
      name: '前端入门到放弃' + i,
      role: i % 2 ? 'MP3' : 'XLSX',
      sex: `${i % 3}`,
      age: i,
      cascader: ['jiangsu', 'nanjing', 'zhonghuamen'],
      quarter: '2019-05-10',
      hobby: [i % 4],
      switch: Boolean(i % 2),
      checkbox: Boolean(i % 2),
      treeSelect: 'nanjing',
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
        for (let i = 0; i < 200; i++) {
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
