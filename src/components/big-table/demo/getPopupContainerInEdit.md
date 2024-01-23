<cn>
#### 表格编辑为弹出框组件
本示例编辑时候使用的组件为有弹框组件（如select,date,treeSelect等）的时候，关于弹框容器的设置
注意：
- 通过$xxx来渲染编辑容器的时候，弹框容器是默认在body上的，如要设置在table内，需要设置 edit-render.dropDownInBody 为false，并且设置getPopupContainer为表格内
- 通过插槽的形式来渲染编辑容器的时候，弹框默认也是在body上的，但是此时必须要给弹框容器设置一个样式类 "ignore-clear" 才可。
</cn>

<us>
#### complex edit
complex edit
</us>

```html
<template>
    <div>
        <ta-big-table
                ref="xTable"
                border
                height="300px"
                resizable
                keep-source
                show-overflow
                :data="tableData"
                :edit-config="{trigger: 'click', mode: 'row',showStatus: true}"
                @edit-closed="editClosed"
        >
            <ta-big-table-column type="seq" width="60" fixed="left" />
            <ta-big-table-column field="sex" title="弹框容器在外面（默认）" width="150" collection-type="SEX" :edit-render="{name: '$select'}" />
            <ta-big-table-column field="hobby" width="220px" title="弹框容器在里面" :edit-render="{name: '$select',dropDownInBody: false, props: {maxTagCount: 2,mode: 'multiple',options: hobbyList,getPopupContainer:getPopupContainer}}" />
            <ta-big-table-column field="year" title="Year默认在外面" width="150" :edit-render="{name: '$year-picker', props: {format: 'YYYY年'}}" />
            <ta-big-table-column field="treeSelect" title="插槽自定义编辑弹框在表格外面" width="300" :edit-render="{}">
                <template #edit="{row}">
                    <ta-tree-select v-model="row.treeSelect" :tree-data="addressList" dropdown-class-name="ignore-clear" />
                </template>
            </ta-big-table-column>
            <ta-big-table-column field="treeSelect1" title="插槽自定义编辑弹框在表格里面" width="300" :edit-render="{}">
                <template #edit="{row}">
                    <ta-tree-select v-model="row.treeSelect1" :get-popup-container="getPopupContainer" :tree-data="addressList" />
                </template>
            </ta-big-table-column>
        </ta-big-table>
    </div>
</template>

<script >
    const hobbyList = [{ label: '足球', value: 0, }, { label: '篮球', value: 1, }, { label: '排球', value: 2, }, { label: '乒乓球', value: 3, }]
    const addressList = [{
        value: 'zhejiang',
        label: '浙江',
        children: [{
            value: 'hangzhou',
            label: '杭州',
            children: [{
                value: 'xihu',
                label: '西湖',
            }],
        }],
    }, {
        value: 'jiangsu',
        label: '江苏',
        children: [{
            value: 'nanjing',
            label: '南京',
            children: [{
                value: 'zhonghuamen',
                label: '中华门',
            }],
        }],
    }]

    const data = []
    for (let i = 0; i < 6; i++) {
        data.push({
            key: i.toString(),
            sex: `${i % 3}`,
            hobby: [i % 4],
            treeSelect: 'nanjing',
            treeSelect1: 'hangzhou',
            year: '2019-05-10',
        })
    }
    export default {
        data () {
            return {
                tableData: data,
                hobbyList,
                addressList,
            }
        },
        methods: {
            getPopupContainer (trigger) {
                return trigger.parentNode
            },
            editClosed ({ row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, }) {
                this.$refs.xTable.validate([row]).then(() => {
                    console.log({ row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, })
                }).catch(() => {
                    this.$refs.xTable.revertData([row], column.property)
                })
            },
        },
    }
</script>
```
