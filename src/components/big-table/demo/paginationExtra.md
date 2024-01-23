<cn>
#### 分页附加功能
- ta-big-table通过 seq-config={startIndex} 属性设置起始值，支持动态序号
- ta-big-table通过设置 checkbox-config 的 reserve 属性，支持切换页保留选中状态
- 启用 reserve 功能需要有 row-id 唯一主键，可以通过调用 getCheckboxReserveRecords 方法获取获取已保留选中的行数据
</cn>

<us>
#### pagination extra
pagination extra
</us>

```html
<template>
  <div>
    <ta-button @click="getCheckRecords" style="margin-bottom: 20px">
      获取选中项
    </ta-button>
    <ta-big-table
      ref="xTable"
      border
      show-overflow
      highlight-hover-row
      row-id="userId"
      :seq-config="{startIndex: (current - 1) * pageSize}"
      :checkbox-config="{reserve: true}"
      height="300"
      :sort-config="{trigger: 'cell'}"
      :data="userList"
    >
      <ta-big-table-column type="checkbox" width="60" />
      <ta-big-table-column type="seq" width="60" />
      <ta-big-table-column field="name" title="name" sortable />
      <ta-big-table-column field="sex" title="Sex" />
      <ta-big-table-column field="loginId" title="账号" />
      <ta-big-table-column field="namePath" title="组织路径" show-overflow />
    </ta-big-table>
    <ta-pagination
      ref="gridPager"
      v-model="current"
      style="text-align: right;margin-top: 10px"
      :data-source.sync="userList"
      :page-size.sync="pageSize"
      url="demo/tableRestService/queryUserByCondition"
    />
  </div>
</template>

<script>

export default {
  data () {
    return {
      userList: [],
      current: 1,
      pageSize: 10,
    }
  },
  mounted(){
    //进入页面后默认查询表格第一页(分页条实例提供了loadData方法会默认查询第一页,并将数据渲染入表格)
    this.$refs.gridPager.loadData()
  },
  methods: {
    getCheckRecords() {
      console.log(this.$refs.xTable.getCheckboxReserveRecords())
    },
  },
}
</script>

```
