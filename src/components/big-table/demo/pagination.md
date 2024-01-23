<cn>
#### 分页
- ta-big-table不自带分页功能,需要配合分页组件pagination使用
- pagination分页组件可以放到big-table的bottomBar中,实现固定在表尾的效果
</cn>

<us>
#### pagination
pagination
</us>

```html
<template>
  <div>
    <ta-big-table
      border
      show-overflow
      highlight-hover-row
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
      <template #bottomBar>
          <ta-pagination
            ref="gridPager"
            style="text-align: right;"
            :data-source.sync="userList"
            url="demo/tableRestService/queryUserByCondition"
          />
      </template>
    </ta-big-table>

  </div>
</template>

<script>

export default {
  data () {
    return {
      userList: [],
    }
  },
  mounted(){
    //进入页面后默认查询表格第一页(分页条实例提供了loadData方法会默认查询第一页,并将数据渲染入表格)
    this.$refs.gridPager.loadData()
  },
}
</script>
```
