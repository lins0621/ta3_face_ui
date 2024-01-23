<cn>
#### 树形表格选中
- ta-big-table的多选状态,通过checkStrictly设置父子节点关联关系(true严格不关联,false严格关联(默认),half半关联(上级可控制下级,下级不能控制上级))
- ta-big-table通过getCheckboxIndeterminateRecords方法获取半选
</cn>

<us>
#### tree table check
tree table check
</us>

```html
<template>
    <div>
      <p style="margin-bottom: 20px;font-weight: 600">radio选中：</p>
      <ta-big-table
        :tree-config="{children: 'children'}"
        :radio-config="{labelField: 'name'}"
        :data="tableData">
        <ta-big-table-column type="radio" title="Name" width="400" tree-node></ta-big-table-column>
        <ta-big-table-column field="size" title="Size"></ta-big-table-column>
        <ta-big-table-column field="type" title="Type"></ta-big-table-column>
        <ta-big-table-column field="date" title="Date"></ta-big-table-column>
      </ta-big-table>
      <p style="margin-bottom: 20px;margin-top:20px;font-weight: 600">checkbox树选中父子严格关联: checkStrictly=false(默认)</p>
      <ta-button @click="getIndeterminateRecords">获取半选</ta-button>
      <ta-big-table
          ref="xTable"
          resizable
          row-id="id"
          :data="tableData"
          :tree-config="{children: 'children'}"
          :checkbox-config="{labelField: 'name', checkRowKeys: ['122000', '20000']}"
          @checkbox-change="selectChangeEvent">
          <ta-big-table-column type="checkbox" title="Sex" width="400" tree-node></ta-big-table-column>
          <ta-big-table-column field="size" title="Size"></ta-big-table-column>
          <ta-big-table-column field="type" title="Type"></ta-big-table-column>
          <ta-big-table-column field="date" title="Date"></ta-big-table-column>
        </ta-big-table>
      <p style="margin-bottom: 20px;margin-top:20px;font-weight: 600">checkbox树选中父子不关联: checkStrictly=true ,该方式默认不显示头部复选框，可以通过 checkbox-config={showHeader} 设置显示</p>
      <ta-big-table
        resizable
        :data="tableData"
        :tree-config="{children: 'children'}"
        :checkbox-config="{labelField: 'name', checkStrictly: true, showHeader: true,}">
        <ta-big-table-column type="checkbox" title="Name" width="280" tree-node></ta-big-table-column>
        <ta-big-table-column field="size" title="Size"></ta-big-table-column>
        <ta-big-table-column field="type" title="Type"></ta-big-table-column>
        <ta-big-table-column field="date" title="Date"></ta-big-table-column>
      </ta-big-table>
        <p style="margin-bottom: 20px;margin-top:20px;font-weight: 600">checkbox树选中父子不关联: checkStrictly=true,在显示头部复选框时,通过isCheckAll属性可控制头部复选框是否可以全选(指当前已加载的数据,如果是异步的树形结构,则新展开的数据不会被选中)</p>
        <ta-big-table
                resizable
                :data="tableData"
                :tree-config="{children: 'children'}"
                :checkbox-config="{labelField: 'name', checkStrictly: true, showHeader: true, isCheckAll: true}">
            <ta-big-table-column type="checkbox" title="Name" width="280" tree-node></ta-big-table-column>
            <ta-big-table-column field="size" title="Size"></ta-big-table-column>
            <ta-big-table-column field="type" title="Type"></ta-big-table-column>
            <ta-big-table-column field="date" title="Date"></ta-big-table-column>
        </ta-big-table>
        <p style="margin-bottom: 20px;margin-top:20px;font-weight: 600">checkbox树选中父子半关联(上级可控制下级,下级不能控制上级):checkStrictly=half </p>
        <ta-big-table
                resizable
                :data="tableData"
                :tree-config="{children: 'children'}"
                :checkbox-config="{labelField: 'name', checkStrictly: 'half'}">
            <ta-big-table-column type="checkbox" title="Name" width="280" tree-node></ta-big-table-column>
            <ta-big-table-column field="size" title="Size"></ta-big-table-column>
            <ta-big-table-column field="type" title="Type"></ta-big-table-column>
            <ta-big-table-column field="date" title="Date"></ta-big-table-column>
        </ta-big-table>
    </div>
</template>
<script>
export default {
  data() {
    return {
      tableData: []
    }
  },
  created() {
    this.tableData = mockTreeData
  },
  methods: {
    getIndeterminateRecords() {
      let IndeterminateRecords = this.$refs.xTable.getCheckboxIndeterminateRecords(true)
      message.info(IndeterminateRecords.length)
    },
    selectChangeEvent ({ records }) {
      console.info(`勾选${records.length}个树形节点`, records)
    }
  }
}
</script>
```
