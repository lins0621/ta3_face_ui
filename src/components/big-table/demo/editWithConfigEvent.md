<cn>
#### 编辑事件处理
- ta-big-table编辑组件的事件回调函数通过edit-render属性内的events对象传入进去，可传递多个回调函数例如:
```javascript
:edit-render="{
    name: '$select', 
    props: {maxTagCount: 2,mode: 'multiple',options: hobbyList}, 
    events: { change: handleChange, select: handleChange }
   }"
```
- 注意：表格编辑时所有的事件回调函数接收的参数都会后移一位，第一个参数始终为`tableInfo`，该参数为表格的信息对象，包括了触发该事件的行信息、行index、列index等等，原本的参数会按照顺序从第二个参数依次传入，例如：
```javascript
// select组件的change事件回调：
// 非表格编辑：
handleChange(value, option){
  // do something...
},
// 表格编辑:
handleChange(tableInfo, value, option){
  console.log(tableInfo)
  // 常用属性
  // tableInfo.$columnIndex    触发当前事件的列索引
  // tableInfo.$rowIndex       触发当前事件的行索引
  // tableInfo.row             触发当前事件的行数据
  // do something...
},
```
</cn>

<us>
#### complex edit with event
complex edit
</us>

```html
<template>
  <div>
    <ta-big-table
      ref="xTable"
      border
      height="300px"
      resizable
      keep-source
      show-overflow
      :data="tableData"
      :edit-config="{trigger: 'click', mode: 'row',showStatus: true}"
    >
      <ta-big-table-column type="checkbox" width="60" fixed="left" />
      <ta-big-table-column type="seq" width="60" fixed="left" />
      <ta-big-table-column field="hobby" title="多选下拉" :edit-render="{name: '$select', props: {maxTagCount: 2,mode: 'multiple',options: hobbyList}, events: { select: handleChange }}" />
    </ta-big-table>
  </div>
</template>

<script >
  const hobbyList = [{label: '足球', value: 0, }, {label: '篮球', value: 1, }, {label: '排球', value: 2, }, {label: '乒乓球', value: 3, }]

  const data = []
  for (let i = 0; i < 6; i++) {
    data.push({
      key: i.toString(),
      hobby: [i % 4],
    })
  }
  export default {
    data () {
      const nameValid = ({ cellValue, }) => {
        if (cellValue && (cellValue.length < 3 || cellValue.length > 50)) {
          return new Error('名称长度在 3 到 50 个字符之间')
        }
      }
      return {
        tableData: data,
        hobbyList,
      }
    },
    methods: {
      renderDefaultAge(h, renderOpts, {cellValue, }){
        return cellValue + ' 岁'
      },
      handleChange(tableInfo, val, option){
        console.log(tableInfo, val, option)
      },
    },
  }
</script>


```
