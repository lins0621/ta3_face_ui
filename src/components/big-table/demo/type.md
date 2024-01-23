
<cn>
#### 表格列类型
- `ta-big-table`可通过`type`属性设置的类型
- `type`可以为string类型,可选值为`yesOrNo`/`date`/`operate`
- `type`可以为object,可传入这些类型的具体配置
- 当`type`为`yesOrNo`和`date`时,这两个属性依赖于数据值,所以必须有`field`属性
- `ta-big-table`支持使用`columns`数据传入配置方式type属性
</cn>

<us>
#### extra-type
extra type
</us>

```html
<template>
  <div>
    <h3>通过big-table-column标签构建表格</h3>
    <ta-big-table highlight-hover-row height="400" :data="tableData">
      <ta-big-table-column type="checkbox" />
      <ta-big-table-column type="yesOrNo" field="effective" title="有效" />
      <ta-big-table-column title="日期" type="date" field="date" />
      <!-- 自定义日期格式 -->
      <ta-big-table-column title="日期(自定义格式)" type="date" format='YYYY年MM月DD日' field="date" />
      <!-- 操作列类型 -->
      <ta-big-table-column type='operate' :operate='operate' title="操作列" />
    </ta-big-table>
    <h3>通过columns属性构建表格</h3>
    <ta-big-table height="400" :columns="tableColumns" :data="tableData" />
  </div>
</template>
<script lang="jsx">
const operateMenu = [
  {
    name: '一个超长的操作菜单名称',
    icon: 'edit',
    onClick: (record, index) => {
      console.log(record)
      message.info(JSON.stringify(record))
      message.info(index)
    },
  },
  {
    name: '删除',
    icon: 'delete',
    type: 'confirm',
    confirmTitle: '确认删除该信息？',
    onOk: (record, index) => {
      message.info('这里调用删除方法')
    },
  }
]
const tableColumns = [
    {
  type: 'checkbox',
  // 等效于下面的对象
  // type: {
  //   type: 'checkbox',
  // },
}, {
  type: 'yesOrNo',
  // 等效于下面的代码
  // type: {
  //   type: 'yesOrNo',
  // },
  field: 'effective',
  title: '有效',
}, {
  type: {
    type: 'yesOrNo',
    // 自定义值的判断方法,返回true时会显示为'是'
    // 此处演示的方法于前一列的渲染显示完全相反
    customFlag (value) {
      return value === '0'
    },
    // 自定义tag的样式
    customStyle: 'border-color: blue;',
    // 自定义tag的class
    customClass: 'custom-yes-or-no-class',
    // 自定义customFlag为true时的显示文本
    customYes: '是的',
    // 自定义customFlag为false时的显示文本
    customNo: '不是',
  },
  field: 'effective',
  title: '有效(自定义元素)',
}, {
  type: {
    type: 'yesOrNo',
    // 当使用自定义render的时候,可以完全自定义当前单元格所显示的值的渲染
    customRender (h, v) {
      const style = 'border: 1px dashed red;'
      return (
        <span style >{v === '1' ? '确定' : '否认'}</span>
      )
    },
  },
  field: 'effective',
  title: '有效(自定义渲染)',
}, {
  type: 'date',
  // 等效于下面的代码
  // type: {
  //   type: 'date',
  // },
  field: 'date',
  title: '日期',
}, {
  type: 'date',
  // 定义日期格式化参数,默认值为YYYY-MM-DD
  format: 'YYYY年MM月DD日',
  // 等效于下面的代码
  // type: {
  //   type: 'date',
  //   format: 'YYYY-MM-DD',
  // },
  field: 'date',
  title: '日期(自定义格式)',
}, {
  type: {
    type: 'date',
    customRender (h, v) {
      return (
        <span>自定义的日期: { v }</span>
      )
    },
  },
  field: 'date1',
  title: '日期(自定义渲染)',
}, {
  type: 'operate',
  operate: {
    operateMenu,
    overflowTooltip: true,
  },
  title: '操作列',
  // 等效与下列代码
  // type: {
  //   type: 'operate',
  //   operate: {
  //     operateMenu: [],
  //   },
  // }
}, {
  type: {
    type: 'operate',
    // 自定义操作列渲染方式
    customRender (h, v) {
      return (
        <span>自定义操作列</span>
      )
    },
  },
  title: '操作列(自定义渲染)',
}]

export default {
  data () {
    return {
      operateMenu,
      operate: { operateMenu: operateMenu, overflowTooltip: true, },
      loading: false,
      tableData: [],
      tableColumns,
      sexList: [
        {
          label: '女',
          value: '2',
        },
        {
          label: '男',
          value: '1',
        }
      ],
    }
  },
  created () {
    this.tableData = [
      { id: 10001, date: '2022-02-02', date1: '2022-02-02', effective: '1', },
      { id: 10002, date: '2022/12/31', date1: '2022/12/31', effective: '0', },
      { id: 10003, date: '12/13/2022', date1: '12/13/2022', effective: '1', },
      { id: 10004, date: '2022.1.2', date1: '2022.1.2', effective: '0', },
      { id: 10005, date: Date.now(), date1: Date.now(), effective: '1', },
      { id: 10006, date: '2022/1/18 10:05', date1: '2022/1/18 10:05', effective: '0', },
      { id: 10007, date: 'Wed Aug 24 2016 22:26:19 GMT+0800', date1: 'Wed Aug 24 2016 22:26:19 GMT+0800', effective: '1', }
    ]
  },
}
</script>
<style>
.custom-yes-or-no-class{
  border-bottom: 0 !important;
}
</style>

```
