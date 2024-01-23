
<cn>
#### 操作列
- ta-big-table的操作列功能配合table-operate组件使用
- ta-big-table的big-table-column提供一个`operate`类型用于简化
</cn>

<us>
#### operate table
operate table
</us>

```html
<template>
  <div>
    <ta-big-table
      ref="plTable"
      :data="tableData"
      :height="height"
      use-virtual
      showBodyOverflow="title"
      showHeaderOverflow="title"
      :row-height="rowHeight"
      border>
      <ta-big-table-column type="index" width="100" fixed/>
      <ta-big-table-column width="100" field="sex" label="性别"/>
      <ta-big-table-column
        v-for="item in columns"
        :key="item.id"
        :resizable="item.resizable"
        :show-overflow-tooltip="item.showOverflow"
        :field="item.prop"
        :title="item.label"
        :fixed="item.fixed"
        :width="item.width"/>
      <ta-big-table-column
        fixed="right"
        field="operate"
        title="操作"
        width="200">
        <template #default='rowInfo'>      
            <ta-table-operate :operate-menu="operateMenu" :rowInfo="rowInfo"/>      
        </template>
      </ta-big-table-column>
      <!-- 也可以使用type='operate'类型 -->
      <!-- <ta-big-table-column type='operate' :operate='{operateMenu: operateMenu,}' fixed='right' width='200' -->
    </ta-big-table>
  </div>
</template>

<script>
export default {
	data() {
		let col = ['id', 'date', 'name', 'address', "age"];
		return {
			height: 500,
			rowHeight: 55,
			columns: col.map((item) => ({prop: item, id: item, label: item, width: 200,})),
			tableData: Array.from({length: 500}, (_, idx) => ({
				id: idx + 1,
				date: '2016-05-03',
				name: 1,
				sex: idx % 2 + '',
				address: '北京市天安门天安门天安门北',
				age: idx + 1,
			})),
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
				},

			],
		}
	}
}
</script>
```
