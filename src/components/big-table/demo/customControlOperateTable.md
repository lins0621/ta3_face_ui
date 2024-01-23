
<cn>
#### 自定义行编辑
- ta-big-table可自定义操作列，自定义控制表格的编辑状态，通过setActiveRow、clearActived等方法来控制。
</cn>

<us>
#### Custom Control Edit Status
You can set the operation column and customize the editing status of the control table by setActiveRow, clearActived and other methods.
</us>

```html
<template>
    <div>
        <ta-big-table
                ref="xTable"
                :data="tableData"
                :height="height"
                use-virtual
                showBodyOverflow="title"
                showHeaderOverflow="title"
                :row-height="rowHeight"
                keep-source
                :edit-config="{trigger: 'manual', mode: 'row',autoClear:false}"
                border>
            <ta-big-table-column type="index" width="100" fixed/>
            <ta-big-table-column
                    :resizable="true"
                    :show-overflow-tooltip="true"
                    field="name"
                    title="姓名"
                    :edit-render="{name: '$input'}"/>
            <ta-big-table-column width="100" field="sex" label="性别" collection-type="sex" :edit-render="{name: '$select',props:{collectionType: 'sex'}}"/>
            <ta-big-table-column
                    :resizable="true"
                    :show-overflow-tooltip="true"
                    field="age"
                    title="年龄"
                    :edit-render="{name: '$input-number'}"/>
            <ta-big-table-column
                    fixed="right"
                    field="operate"
                    title="自定义的操作列">
                <template #default="{row}">
                    <template v-if="editIsActive(row)">
                        <a @click="editSave(row)">
                            保存
                        </a>
                        <ta-divider type="vertical" />
                        <a @click="editCancel(row)">
                            取消
                        </a>
                    </template>
                    <template v-else>
                        <a @click="editActive(row)">
                            修改
                        </a>
                        <ta-divider type="vertical" />
                        <ta-popconfirm
                                title="确认删除该条数据?"
                                ok-text="确认"
                                cancel-text="取消"
                                @confirm="fnDelete(row)"
                        >
                            <a>
                                删除
                            </a>
                        </ta-popconfirm>
                    </template>
                </template>
            </ta-big-table-column>
        </ta-big-table>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                height: 500,
                rowHeight: 55,
                tableData: Array.from({length: 500}, (_, idx) => ({
                    id: idx + 1,
                    date: '2016-05-03',
                    name: '李白' + idx,
                    sex: idx % 2 + '',
                    address: '北京市天安门天安门天安门北',
                    age: idx + 1,
                })),
            }
        },
        methods: {
            editIsActive (row) {
                return this.$refs.xTable.isActiveByRow(row)
            },
            editActive (row) {
                this.$refs.xTable.setActiveRow(row)
            },
            editCancel (row) {
                this.$refs.xTable.revertData(row).then(() => {
                    this.$refs.xTable.clearActived()
                })
            },
            fnDelete (row) {
                console.log('要删除的行为：',row)
            },
            editSave (row) {
                this.$refs.xTable.validate(row).then(() => {
                    // 校验成功 然后判断行是否修改
                    if (!this.$refs.xTable.isUpdateByRow(row)) {
                        message.info('数据未有改动')
                        return
                    }
                    // 此处可以发送数据至后端进行保存
                    // Base.submit......
                    this.$refs.xTable.clearActived()
                }).catch(errMap => {
                    errMap && message.error('校验不通过！')
                })
            },
        },
    }
</script>
```
