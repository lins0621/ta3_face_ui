
<cn>
#### 列控制
- ta-big-table通过 control-column 属性进行列控制，可进行列的显示隐藏和列的拖拽顺序，具体[配置查看](process.env.VUE_APP_PUBLIC_PATH/components/big-table-cn/#列控制配置)
</cn>

<us>
#### Columns Control
Set the control column attribute to control
</us>
    
```html
<template>
    <div>
        <ta-button @click="open">
            打开列控制
        </ta-button>
        <ta-big-table
                ref=xTable
                border
                stripe
                resizable
                highlight-hover-row
                height="400"
                :export-config="{}"
                :import-config="{}"
                :control-column="showHiddenOrSortColumn"
                :data="tableData"
        >
            <ta-big-table-column type="seq" width="60" />
            <ta-big-table-column field="name" title="Name" sortable />
            <ta-big-table-column field="sex" title="Sex" collection-type="SEX" />
            <ta-big-table-column field="address" title="Address" show-overflow />
            <ta-big-table-column field="abc" title="abc" show-overflow />
        </ta-big-table>
    </div>
</template>
<script>
    export default {
        data () {
            return {
                // 列编辑配置
                showHiddenOrSortColumn: {
                    // 主题颜色
                    themeColor: 'red',
                    // 自定义的按钮图标
                    icon: 'appstore',
                    // 显示隐藏列配置
                    showHiddenConfig: {
                        open: true,
                        // disabledHiddenColumns: ['seq', 'sex'], // 不允许显示隐藏的列,传入field或type
                        disabledHiddenColumns: (column) => { // 返回true则不允许显示隐藏
                            return false
                        },
                    },
                    // 列拖拽排序配置
                    columnSortConfig: {
                        open: true,
                        onMove: (e, { dragColumn, dropColumn, }) => {
                            // 不允许拖拽sex列,此处控制是否允许拖动
                            // if (dragColumn.property === 'sex') return false
                            return true
                        },
                        dragEnd: (e, { dragColumn, resultColumns, }) => {
                            // 拖拽结束
                            console.log('拖拽结束,拖拽的列，拖拽后的列列表情况', { dragColumn, resultColumns, })
                        },
                    },
                    // 点击确定的回调，传回列的列表
                    successCallback: this.successCallback,
                    // 不显示在面板的列，返回true则不显示，注：隐藏的列会一直跟在最初的前面列后面
                    disabledControlCol: (column) => {
                        // 不让sex列和seq列显示在面板上
                        return column.property === 'sex' || column.type === 'seq'
                    },
                    // 自定义的按钮
                    footerButtonRender: {
                        // 如果不需要显示可以设置为null
                        // resetRender: null,  // 不需要显示这个按钮的话，直接设置为null
                        // jsx 语法
                        // resetRender: () => {
                        //     return (<ta-button size="small">重置自定</ta-button>)
                        // },
                        // render函数
                        resetRender: () => {
                            return this.$createElement('ta-button', {
                                attrs: {
                                    size: 'small'
                                },
                            },'重置自定');
                        },
                        // cancelRender: () => {
                        //   return (<ta-button size="small">取消哦</ta-button>)
                        // },
                        // confirmRender: () => {
                        //   return (<ta-button size="small" type="primary">确认哦</ta-button>)
                        // },
                    },
                },
                loading: false,
                tableData: [
                    { id: 10001, name: 'Test1', role: 'Develop', sex: '1', age: 28, address: 'ta-big-table 从入门到放弃', },
                    { id: 10002, name: 'Test2', role: 'Test', sex: '2', age: 22, address: 'Guangzhou', },
                    { id: 10003, name: 'Test3', role: 'PM', sex: '1', age: 32, address: 'Shanghai', },
                    { id: 10004, name: 'Test4', role: 'Designer', sex: '2', age: 23, address: 'ta-big-table 从入门到放弃', },
                    { id: 10005, name: 'Test5', role: 'Develop', sex: '1', age: 30, address: 'Shanghai', },
                    { id: 10006, name: 'Test6', role: 'Designer', sex: '2', age: 21, address: 'ta-big-table 从入门到放弃', },
                    { id: 10007, name: 'Test7', role: 'Test', sex: '1', age: 29, address: 'ta-big-table 从入门到放弃', },
                    { id: 10008, name: 'Test8', role: 'Develop', sex: '2', age: 35, address: 'ta-big-table 从入门到放弃', }
                ],
            }
        },
        methods: {
            open () {
                this.$refs.xTable.openColumnsControl()
            },
            successCallback ({ table, resultColumnsList, }) {
                // 返回最终的列情况，visible为是否显示
                console.log('点击确定的回调，确定后的列情况', { table, resultColumnsList, })
            },
        },
    }
</script>
```
