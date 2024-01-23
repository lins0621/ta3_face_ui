
<cn>
#### 数据列自定义渲染
- ta-big-table可以通过 columns 属性传入数组生成表格列的自定义渲染
- ta-big-table配置列的customRender属性用于自定义渲染
</cn>

<us>
#### custom column by data 
</us>

```html
<template>
  <div>
    <ta-big-table
      ref="xTable"
      border
      stripe
      resizable
      highlight-hover-row
      height="400"
      :checkbox-config="{labelField: 'id', highlight: true, range: true}"
      :edit-config="{trigger: 'click'}"
      :data="tableData"
      :columns="tableColumns"
    >
      <template #name="{row}">
        自定name显示的模板-{{ row.name }}
      </template>
      <template #nameHeader="{row,column}">
        自定义name表头的模板
      </template>
      <template #nameEdit="{row,column}">
        自定义name编辑
        <ta-input v-model="row.name" />
      </template>
      <template #roleEdit="{row,column}">
        自定义的role编辑
        <ta-select id="customSelect" v-model="row.role" class="custom-select" :get-popup-container="setContainer">
          <ta-select-option value="猪">
            猪
          </ta-select-option>
          <ta-select-option value="狗">
            狗
          </ta-select-option>
          <ta-select-option value="牛">
            牛
          </ta-select-option>
        </ta-select>
        <ta-icon type="user" />
      </template>
      <template #columnGroupHeader>
        这是自定义列分组的表头
      </template>
      <template #operate="rowInfo">
        <ta-table-operate :operate-menu="operateMenu" :row-info="rowInfo" />
      </template>
    </ta-big-table>
  </div>
</template>
<script>
export default {
  data () {
    return {
      // 列配置
      tableColumns: [
        { type: 'seq', title: '序号', width: '60', },
        {
          field: 'name',
          title: 'Name',
          width: '280',
          // 所有编辑需要传入editRender
          editRender: {},
          // 所有自定义需要传入customRender对象
          customRender: {
            default: 'name', // 默认渲染的slot
            // header: 'nameHeader',// header的slot
            // footer: 'nameFooter', // footer的slot
            edit: 'nameEdit', // 编辑的slot
            // filter: 'nameFilter', // 过滤的slot
            // default: ({ row, }) => { // 自定义的jsx风格的渲染
            //   return (<span>{row.name}来了老弟</span>)
            // },
          },
        },
        {
          title: '最上的标题',
          customRender: {
            // 自定义的分组表头
            header: 'columnGroupHeader',
          },
          children: [
            {
              field: 'role',
              title: 'Role',
              width: '280',
              editRender: {},
              customRender: {
                edit: 'roleEdit',
              },
            },
            { field: 'phone', title: 'phone', width: '280', sortable: true, }
          ],
        },
        { field: 'address', title: 'Address', width: '280', fixed: 'right', },
        {
          field: 'operate',
          title: '操作列',
          width: '280',
          fixed: 'right',
          customRender: {
            // 操作列的slot
            default: 'operate',
          },
        }
      ],
      tableData: [],
      operateMenu: [
        {
          name: '编辑',
          icon: 'edit',
          onClick: (record, index) => {
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

      ],
    }
  },
  created () {
    setTimeout(() => {
      this.tableData = [
        {
          id: 10001,
          name: 'Test1',
          role: 'Develop',
          sex: '1',
          phone: '13312439876',
          age: 28,
          address: 'ta-big-table 从入门到放弃',
        },
        { id: 10002, name: 'Test2', role: 'Test', sex: '2', phone: '13312439876', age: 22, address: 'Guangzhou', },
        { id: 10003, name: 'Test3', role: 'PM', sex: '1', phone: '13312439876', age: 32, address: 'Shanghai', },
        {
          id: 10004,
          name: 'Test4',
          role: 'Designer',
          sex: '2',
          phone: '13312439876',
          age: 23,
          address: 'ta-big-table 从入门到放弃',
        },
        { id: 10005, name: 'Test5', role: 'Develop', sex: '1', phone: '13312439876', age: 30, address: 'Shanghai', },
        {
          id: 10006,
          name: 'Test6',
          role: 'Designer',
          sex: '2',
          phone: '13312439876',
          age: 21,
          address: 'ta-big-table 从入门到放弃',
        },
        {
          id: 10007,
          name: 'Test7',
          role: 'Test',
          sex: '1',
          phone: '13312439876',
          age: 29,
          address: 'ta-big-table 从入门到放弃',
        },
        {
          id: 10008,
          name: 'Test8',
          role: 'Develop',
          sex: '2',
          phone: '13312439876',
          age: 35,
          address: 'ta-big-table 从入门到放弃',
        }
      ]
    }, 500)
  },
  methods: {
    // 必须设置弹框容器为其父节点，否则会在失去焦点之前就会注销组件导致不会触发自定义组件的change事件
    setContainer (trigger) {
      return document.getElementById('customSelect').parentNode
    },
  },
}
</script>

```
