
<cn>
#### 行拖拽排序
ta-big-table通过`draggable`属性配置开启行拖拽功能,其配置有如下的一些规则
- `draggable`支持`Boolean`和`{needRefresh: Boolean}`两种类型的配置
- 若`draggable`设置为`true`时,表示当前表格支持行拖拽及拖拽后会同步更新表格数据排序
- 若`draggable`设置为`{needRefresh: true}`,与将`draggable`设置为`true`时行为一致
- 若`draggable`设置为`false`时,表示当前表格不支持行拖拽
- 若`draggable`设置为`{needRefresh: false}`,表示当前表格仅支持行拖拽,拖拽后的排序不会被同步到表格数据中
- `draggable`属性也支持在配置中传入事件回调(包括`onStart`/`onAdd`/`onRemove`/`onUpdate`/`onEnd`/`onChoose`/`onUnchoose`/`onSort`/`onClone)回调
- `draggable`属性的内部实现使用了`onEnd`事件回调进行表格数据排序的同步(如果`needRefresh`为`true`时),所以,`onEnd`事件实际可能会在表格数据同步更新后才会触发
</cn>

<us>
#### data line draggable
data line draggable
</us>

```html
<template>
    <div>
        <ta-button @click='click'>
            获取拖拽后的表格数据
        </ta-button>
        <ta-big-table
                ref='rTable'
                border
                stripe
                resizable
                highlight-hover-row
                height='400'
                :checkbox-config="{labelField: 'id', highlight: true, range: true}"
                :data='tableData'
                :draggable='draggable'
        >
            <ta-big-table-column type='seq' width='60' />
            <ta-big-table-column type='checkbox' title='ID' width='140' />
            <ta-big-table-column field='name' title='Name' sortable />
            <ta-big-table-column field='sex' title='Sex' collection-type='SEX' />
            <ta-big-table-column
                    field='age'
                    title='Age'
                    sortable
            />
            <ta-big-table-column field='address' title='Address' show-overflow />
        </ta-big-table>
    </div>
</template>
<script>
    export default {
        data () {
            return {
                loading: false,
                tableData: [],
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
                // draggable: true,
                draggable: {
                    needRefresh: true,
                    onEnd: (e) => {
                        const { oldIndex, newIndex, } = e
                        console.log('drop-end', oldIndex, newIndex)
                    },
                    onStart: (e) => {
                        console.log('drop-start', e)
                    },
                },
            }
        },
        created () {
            setTimeout(() => {
                this.tableData = [
                    { id: 10001, name: 'Test1', role: 'Develop', sex: '1', age: 28, address: 'ta-big-table 从入门到放弃', },
                    { id: 10002, name: 'Test2', role: 'Test', sex: '2', age: 22, address: 'Guangzhou', },
                    { id: 10003, name: 'Test3', role: 'PM', sex: '1', age: 32, address: 'Shanghai', },
                    { id: 10004, name: 'Test4', role: 'Designer', sex: '2', age: 23, address: 'ta-big-table 从入门到放弃', },
                    { id: 10005, name: 'Test5', role: 'Develop', sex: '1', age: 30, address: 'Shanghai', },
                    { id: 10006, name: 'Test6', role: 'Designer', sex: '2', age: 21, address: 'ta-big-table 从入门到放弃', },
                    { id: 10007, name: 'Test7', role: 'Test', sex: '1', age: 29, address: 'ta-big-table 从入门到放弃', },
                    { id: 10008, name: 'Test8', role: 'Develop', sex: '2', age: 35, address: 'ta-big-table 从入门到放弃', }
                ]
            }, 500)
        },
        methods: {
            click () {
                console.log(this.$refs.rTable.getTableData().fullData)
            },
        },
    }
</script>

```
