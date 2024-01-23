
<cn>
#### 隐藏列至展开中
- ta-big-table通过control-column的 `showHiddenConfig.hideInExpand: true` 设置列隐藏时将其收缩到列展开中
- ta-big-table需要设置 expand 列，expand 列不设置content插槽即可。如下示例
</cn>

<us>
#### Hide columns in expansion
Set the control column attribute to control
</us>

```html
<template>
    <div>
        <ta-button @click="open">
            打开列控制，列控制隐藏列后会将列的信息放入展开中
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
                class="xTable"
        >
            <ta-big-table-column type="seq" width="60" />
            <ta-big-table-column type="expand"  title="详细" width="60" />
            <ta-big-table-column field="name" width="120" title="Name" sortable :edit-render="{name: '$input'}" />
            <ta-big-table-column field="sex" width="120" title="Sex" collection-type="SEX" />
            <ta-big-table-column field="address" width="120" title="Address" show-overflow />
            <ta-big-table-column field="id" width="220" title="ID" show-overflow >
                <template #default="{row}">
                    <span>我是</span>
                    <span>自定义的{{row.id}}</span>
                </template>
            </ta-big-table-column>
            <ta-big-table-column field="role" width="120" title="Role" show-overflow />
            <ta-big-table-column field="abc" width="120" title="第一" show-overflow />
            <ta-big-table-column field="abcd" width="120" title="第二" show-overflow />
            <ta-big-table-column field="abcde" width="120" title="第三" show-overflow />
            <ta-big-table-column field="abcdef" width="120" title="第四" show-overflow />
            <ta-big-table-column field="h1" title="H一" width="120" show-overflow />
            <ta-big-table-column field="h2" title="H二" width="120" show-overflow />
            <ta-big-table-column field="h3" title="H三" width="120" show-overflow />
            <ta-big-table-column field="h4" title="H四" width="120" show-overflow />
            <ta-big-table-column field="h5" title="H五" width="120" show-overflow />
            <ta-big-table-column field="h6" title="H刘" width="120" show-overflow />
            <ta-big-table-column field="h7" title="H起" width="120" show-overflow />
            <ta-big-table-column field="h8" title="H八" width="120" show-overflow />
            <ta-big-table-column field="h9" title="H久" width="120" show-overflow />
            <ta-big-table-column field="h10" title="H时" width="120" show-overflow />
            <ta-big-table-column field="h11" title="H十一" width="120" show-overflow />
        </ta-big-table>
    </div>
</template>
<script>
    const tableData = Array.from({ length: 15, },(i,index) => {
        return {
            id: 10001 + index,
            name: 'Test' + index,
            role: 'Develop',
            sex: index % 2 + '',
            age: 2 + index,
            address: 'ta-big-table 从入门到放弃',
            abc: '哈哈哈',
            abcd: '你好',
            abcde: '你好娃娃',
            abcdef: '00阿斯加德',
            h1: '啊啊啊',
            h2: '你好你好你你好你好你你好你好你你好你好你',
            h3: '啊啊啊',
            h4: 'acd',
            h5: '啊啊啊',
            h6: '你好你好你你好你好你你好你好你你好你好你',
            h7: '啊啊啊',
            h8: 'acd',
            h9: '你好你好你你好你好你你好你好你你好你好你',
            h10: '啊啊啊',
            h11: 'acd',
        }
    })

    console.log('0000--',tableData)
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
                        // 隐藏后是否收缩到expand中，启用此会出现一个展开列,如果不写content插槽会使用默认的插槽
                        hideInExpand: true,
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
                        return column.type === 'expand' || column.type === 'seq'
                    },
                },
                loading: false,
                tableData: tableData,
            }
        },
        mounted () {
            this.$nextTick(() => {
                // this.$refs.xTable.hideColumn(this.$refs.xTable.getColumnByField('sex'))
            })
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
<style scoped lang="less">
    .xTable /deep/ .vxe-expand-default-item{
        margin-right: 20px;
    .vxe-expand-item-title {
        color: red;
    }
    .vxe-expand-item-value {
        color: #2baee9;
    }
    }
</style>
```
