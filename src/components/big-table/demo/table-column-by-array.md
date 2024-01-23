
<cn>
#### 表格列通过数组生成
- ta-big-table可通过 columns 属性传入数组生成表格列，类似于旧的 table 组件
- columns为对象数组，里面的属性除了customRender和children属性外，都是ta-big-table-column的API属性
- customRender 属性是用于自定义模板渲染的，一般有 header、default、footer、edit、filter，参考ta-big-table-column的插槽即可
- 如果需要表头分组,则可以将children传入即可。
</cn>

<us>
#### Generate a list through data, generate a grid through an array
The columns attribute is passed into the array to generate table columns, similar to the old table component
Careful:
- Columns: An object array is passed in. The attributes in the array are all the API attributes of ta big table column except the customRender and children attributes
- The customRender attribute is used to customize template rendering, which generally includes header, default, footer, edit, and filter. Just refer to the slot of ta big table column
- If header grouping is required, children can be passed in.
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
                :data="tableData"
                :columns="tableColumns"
        >
            <template #nameDefault="{row}">
                自定义模板-{{ row.name }}
            </template>
            <template #nameHeader="{row,column}">
                自定义的name表头
            </template>
            <template #columnGroupHeader>
                这是列分组的表头
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
                        customRender: {
                            //default: 'nameDefault',
                            header: 'nameHeader',
                            footer: 'nameFooter',
                            edit: 'nameEdit',
                            filter: 'nameFilter',
                            default: ({ row, }) => {
                                // jsx语法
                                // return (<span>{row.name}来了老弟</span>)
                                // render函数语法
                                return this.$createElement('span', {}, `${row.name}来了老弟`);
                            },
                        },
                    },
                    {
                        title: '最上的标题',
                        customRender: {
                            header: 'columnGroupHeader',
                        },
                        children: [
                            { field: 'role', title: 'Role', width: '280', },
                            { field: 'phone', title: 'phone', width: '280', sortable: true, }
                        ],
                    },
                    { field: 'address', title: 'Address', width: '280',  fixed: 'right', }
                ],
                tableData: [],
            }
        },
        created () {
            setTimeout(() => {
                this.tableData = [
                    { id: 10001, name: 'Test1', role: 'Develop', sex: '1', phone: '13312439876', age: 28, address: 'ta-big-table 从入门到放弃', },
                    { id: 10002, name: 'Test2', role: 'Test', sex: '2', phone: '13312439876', age: 22, address: 'Guangzhou', },
                    { id: 10003, name: 'Test3', role: 'PM', sex: '1', phone: '13312439876', age: 32, address: 'Shanghai', },
                    { id: 10004, name: 'Test4', role: 'Designer', sex: '2', phone: '13312439876', age: 23, address: 'ta-big-table 从入门到放弃', },
                    { id: 10005, name: 'Test5', role: 'Develop', sex: '1', phone: '13312439876', age: 30, address: 'Shanghai', },
                    { id: 10006, name: 'Test6', role: 'Designer', sex: '2', phone: '13312439876', age: 21, address: 'ta-big-table 从入门到放弃', },
                    { id: 10007, name: 'Test7', role: 'Test', sex: '1', phone: '13312439876', age: 29, address: 'ta-big-table 从入门到放弃', },
                    { id: 10008, name: 'Test8', role: 'Develop', sex: '2', phone: '13312439876', age: 35, address: 'ta-big-table 从入门到放弃', }
                ]
            }, 500)
        },
    }
</script>
```
