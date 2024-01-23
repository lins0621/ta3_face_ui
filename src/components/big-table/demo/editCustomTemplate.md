<cn>
#### 自定义编辑组件
- ta-big-table可实现自定义列编辑,本示例为自定义编辑组件
- 自定义的编辑组件如弹出框是在body上，则需要设置弹框组件(一般为dropdownClassName属性)的弹框class为：'ignore-clear'
- 需要使用big-table-column的edit插槽来使用自定义组件
- ta-big-table-column 标签必须设置edit-render属性，即使没有也要传{}
- 在使用有弹出框等组件时，如果需要把弹出框挂载到跟组件同级下，则需要给弹出框设置类名为： `ignore-clear`,否则不会触发change事件导致更改失败
</cn>

<us>
#### custom edit
custom edit
</us>

```html
<template>
    <div>
        <ta-button @click="addRow">
            添加临时行
        </ta-button>
        <ta-button @click="removeRow">
            删除首行
        </ta-button>
        <ta-button @click="sureAdd">
            确认添加后，新添加的行才不是临时行，编辑是可以保存状态
        </ta-button>
        <ta-button @click="getInsertRecords">
            获取添加的行
        </ta-button>
        <ta-button @click="getRemoverow">
            获取删除的行
        </ta-button>
        <ta-button @click="getRecordset">
            获取相关数据
        </ta-button>
        <div>
            <ta-big-table
                    ref="xTable"
                    border
                    show-overflow
                    keep-source
                    :data="tableData"
                    :edit-config="{trigger: 'click', mode: 'cell', showStatus: true}"
            >
                <ta-big-table-column type="seq" width="60" />
                <ta-big-table-column field="role" title="Role" :edit-render="{autofocus: '.custom-select',renderCell: renderRole }">
                    <template #edit="{ row }">
                        <ta-select id="customSelect" v-model="row.role" style="width: 100%" class="custom-select" :get-popup-container="setContainer">
                            <ta-select-option value="猪">
                                猪
                            </ta-select-option>
                            <ta-select-option value="狗">
                                狗
                            </ta-select-option>
                            <ta-select-option value="牛">
                                牛
                            </ta-select-option>
                        </ta-select>
                    </template>
                </ta-big-table-column>
                <ta-big-table-column field="sex" title="弹出框是在body的" :edit-render="{}">
                    <template #edit="{ row }">
                        <ta-select v-model="row.sex" style="width: 100%" class="custom-select" dropdown-class-name="ignore-clear">
                            <ta-select-option value="男">
                                男
                            </ta-select-option>
                            <ta-select-option value="女">
                                女
                            </ta-select-option>
                            <ta-select-option value="不男不女">
                                不男不女
                            </ta-select-option>
                        </ta-select>
                    </template>
                </ta-big-table-column>
                <ta-big-table-column field="name" title="Name" :edit-render="{autofocus: '.custom-input'}">
                    <template #edit="{ row }">
                        <ta-input v-model="row.name" class="custom-input" />
                    </template>
                </ta-big-table-column>
                <ta-big-table-column field="age" title="Age" :edit-render="{}">
                    <template #edit="{ row }">
                        <div><ta-input-number v-model="row.age" style="width: 100%" /> </div>
                    </template>
                    <template #default="{row,rowIndex}">
                        <span style="color: indianred">{{ row.age }}</span> <span style="color: #999999">岁</span>
                    </template>
                </ta-big-table-column>
                <ta-big-table-column field="open" title="不同行渲染" :edit-render="{}">
                    <template #edit="{ row, rowIndex }">
                        <template v-if="typeof row.open === 'string'">
                            <ta-input v-model="row.open" placeholder="请输入" />
                        </template>
                        <template v-else-if="typeof row.open === 'boolean'">
                            <ta-switch v-model="row.open" />
                        </template>
                        <template v-else-if="typeof row.open === 'number'">
                            <ta-input-number v-model="row.open" />
                        </template>
                    </template>
                    <template #default="{ row, rowIndex }">
                        <span v-if="typeof row.open === 'string'">{{ row.open }}</span>
                        <span v-else-if="typeof row.open === 'boolean'">{{ row.open ? '打开' : '关闭' }}</span>
                        <span v-else-if="typeof row.open === 'number'">{{ row.open }}</span>
                    </template>
                </ta-big-table-column>
            </ta-big-table>
        </div>
    </div>
</template>
<script>
    const tableData = [
        { role: '道士', name: '张山峰', age: 123, open: '你好哇', sex: '男', },
        { role: '炮王', name: '李云龙', age: 123, open: true, sex: '男', },
        { role: '剑客', name: '陈平安', age: 123, open: 100, sex: '男', },
        { role: '小贼', name: '崔某人', age: 123, open: '1', sex: '男', },
        { role: '土豪', name: '王老五', age: 123, open: '0', sex: '男', }
    ]
    export default {
        data () {
            return {
                tableData,
            }
        },
        methods: {
            // 必须设置弹框容器为其父节点，否则会在失去焦点之前就会注销组件导致不会触发自定义组件的change事件
            setContainer (trigger) {
                return document.getElementById('customSelect').parentNode
            },
            // 使用renderCell进行显示时的渲染
            renderRole (h, renderOpts, { cellValue, }) {
                return '大 ' + cellValue
            },
            addRow () {
                this.$refs.xTable.insert({ role: '土豪', name: '王老五', age: 123, open: '0', sex: '男', })
            },
            removeRow () {
                const firstRow = this.$refs.xTable.afterFullData?.[0]
                this.$refs.xTable.remove(firstRow)
            },
            getRemoverow () {
                console.log('删除的数据', this.$refs.xTable.getRemoveRecords())
            },
            getInsertRecords () {
                console.log('新增的数据', this.$refs.xTable.getInsertRecords())
            },
            getRecordset () {
                console.log('新增的数据', this.$refs.xTable.getRecordset())
            },
            sureAdd () {
                // 调用loadData方法，将临时数据变成原始数据
                const tableData = this.$refs.xTable.getTableData().tableData
                this.$refs.xTable.loadData(tableData)
            },
        },
    }
</script>
```
