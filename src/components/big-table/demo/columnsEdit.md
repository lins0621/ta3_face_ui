
<cn>
#### 列编辑
可以（显示隐藏、拖拽排序）列
在toolbar上通过control-column属性配置来使用
注意：
- themeColor为主题颜色；showHiddenConfig为显示隐藏的配置；columnSortConfig为拖拽排序的配置
- 如若有使用自定义表头，需将ta-big-table-column的title属性加上
</cn>

<us>
#### columns edit
Display, hide or drag and arrange the columns
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
        >
            <template #topBar>
                <ta-big-table-toolbar
                        :import="true"
                        :export="true"
                        :print="true"
                        :custom="true"
                        :control-column="showHiddenOrSortColumn"
                />
            </template>
            <ta-big-table-column type="seq" title="序号" width="60" />
            <ta-big-table-column field="name" title="Name" :disabled-hidden="true" width="300" />
            <ta-big-table-column field="role" title="Role" width="300" />
            <ta-big-table-column field="sex" title="Sex" width="300" />
            <ta-big-table-column field="date" title="Date" fixed="right" width="300" />
            <ta-big-table-column field="address" title="Address" fixed="right" width="300" />
        </ta-big-table>
    </div>
</template>
<script >
    export default {
        data () {
            return {
                // 列编辑配置
                showHiddenOrSortColumn: {
                    themeColor: 'red',
                    showHiddenConfig: {
                        open: true,
                        disabledHiddenColumns: ['seq', 'sex'],
                    },
                    columnSortConfig: {
                        open: true,
                        onMove: (e, { dragColumn, dropColumn, }) => {
                            // 不允许拖拽sex列
                            if (dragColumn.property === 'sex') return false
                            return true
                        },
                        dragEnd: (e, { dragColumn, resultColumns, }) => {
                            // 拖拽结束
                            console.log('拖拽结束,拖拽的列，拖拽后的列列表情况', { dragColumn, resultColumns, })
                        },
                    },
                    // 点击确定的回调，传回列的列表
                    successCallback: this.successCallback,
                },
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
        methods: {
            successCallback (editColumnEnd) {
                console.log('点击确定的回调，确定后的列情况', editColumnEnd)
            },
        },
    }
</script>

```
