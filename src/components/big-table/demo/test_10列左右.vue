<template>
  <!--  正常列 10列左右数据量-->
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
    <ta-big-table-column field="name" title="Name" :edit-render="{name: '$input', props: {autoFocus: true, }}" />
    <ta-big-table-column field="role" title="Role" :edit-render="{name: '$input'}" />
    <ta-big-table-column field="sex" title="Sex" :edit-render="{name: '$select'}" collection-type="SEX" />
    <ta-big-table-column field="age" title="Age" :edit-render="{name: '$input-number'}" />
    <ta-big-table-column field="cascader" title="Cascader" :edit-render="{name: '$cascader', props: {options: addressList}}" />
    <ta-big-table-column field="quarter" title="Quarter" :edit-render="{name: '$quarter-picker', props: {format: 'YYYY年Q季度'}}" />
    <ta-big-table-column field="hobby" title="多选下拉" :edit-render="{name: '$select', props: {maxTagCount: 2,mode: 'multiple',options: hobbyList}}" />
    <ta-big-table-column field="switch" title="Switch" :edit-render="{name: '$switch', trueText: '有效', falseText: '无效'}" />
    <ta-big-table-column field="checkbox" title="Checkbox" :edit-render="{name: '$checkbox'}" />
    <ta-big-table-column field="treeSelect" title="TreeSelect" :edit-render="{name: '$tree-select', showPath: true, props: {treeData: addressList}}" />
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
      id: i,
      name: 'Test' + i,
      role: i % 2 ? '前端' : '后端',
      sex: `${i % 3}`,
      age: i,
      cascader: ['jiangsu', 'nanjing', 'zhonghuamen'],
      quarter: '2019-05-10',
      hobby: [i % 4],
      switch: Boolean(i % 2),
      checkbox: Boolean(i % 2),
      treeSelect: 'nanjing',
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
        tableData,
        hobbyList,
        addressList,
        validRules: {
          name: [
            { required: true, message: '姓名必须填', },
            { validator: nameValid, }
          ],
          role: [
            { validator: roleValid, }
          ],
          sex: [
            { required: true, message: '性别必须填写', }
          ],
          age: [
            { pattern: '^[0-9]{0,3}$', message: '格式不正确', }
          ],
        },
      }
    },
  }
</script>
