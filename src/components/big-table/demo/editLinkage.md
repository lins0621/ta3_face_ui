
<cn>
#### 表格编辑联动
- ta-big-table表格编辑列之间可实现联动,这样可实现列之间的数据控制
</cn>

<us>
#### Table editing linkage
Linkage between table edit columns
</us>

```html
<template>
    <div>
        <ta-big-table
                ref="xTable"
                border
                height="400px"
                resizable
                keep-source
                show-overflow
                :data="tableData"
                :edit-config="{trigger: 'click', mode: 'row',showStatus: true}"
        >
            <ta-big-table-column type="checkbox" width="60" fixed="left" />
            <ta-big-table-column type="seq" width="60" fixed="left" />
            <ta-big-table-column field="name" title="Name" width="150" :edit-render="{name: '$input', props: {autoFocus: true, }}" />
            <ta-big-table-column field="age" title="Age" width="150">
                <template #default="{ row }">
                    <span>{{ row.name }} 的长度是 {{ row.name.length }}</span>
                </template>
            </ta-big-table-column>
            <ta-big-table-column field="sex" title="Sex" width="150" collection-type="SEX" :edit-render="{}">
                <template #edit="{row}">
                    <ta-select
                            style="width: 100%"
                            collection-type="SEX"
                            dropdown-class-name="ignore-clear"
                            :value="row.sex"
                            @change="(value) => changeSex(row,value)"
                    />
                </template>
            </ta-big-table-column>
            <ta-big-table-column
                    field="hobby"
                    width="220px"
                    title="爱好"
                    :edit-render="{}"
            >
                <template #default="{row}">
                    <span>{{ row.hobby[0] === 0 ? '洗浴' : '化妆' }}</span>
                </template>
                <template #edit="{row}">
                    <ta-select
                            id="customSelect"
                            dropdown-class-name="ignore-clear"
                            :get-popup-container="setContainer"
                            :value="getValue(row)"
                            :options="hobbyList"
                            @change="(value) => change(row,value)"
                    />
                </template>
            </ta-big-table-column>
        </ta-big-table>
    </div>
</template>
<script >
    const hobbyList = [{ label: '洗浴', value: 0, }, { label: '化妆', value: 1, }]
    const data = []
    for (let i = 0; i < 6; i++) {
        data.push({
            key: i.toString(),
            name: `Name ${i}`,
            age: i,
            sex: `${i % 2 + 1}`,
            hobby: [i % 2],
        })
    }
    export default {
        data () {
            return {
                tableData: data,
                hobbyList,
            }
        },
        methods: {
            changeSex(row, value) {

                if (value === '1') {
                    row.hobby = [0]
                } else {
                    row.hobby = [1]
                }
                row.sex = value
            },
            change (row, value) {
                row.sex = value === 0 ? '1' : '2'
                row.hobby[0] = value
            },
            // 必须设置弹框容器为其父节点，否则会在失去焦点之前就会注销组件导致不会触发自定义组件的change事件
            setContainer (trigger) {
                return document.getElementById('customSelect').parentNode
            },
            getValue (row) {
                if (row.sex === '1') {
                    return '洗浴'
                }
                return '化妆'
            },
        },
    }
</script>
```
