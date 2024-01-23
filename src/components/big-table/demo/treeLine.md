
<cn>
#### 树形连接线
- ta-big-table的树形形式,支持连接线,通过设置tree-config的`line: true`来实现
</cn>

<us>
#### line
line
</us>

```html
<template>
    <ta-big-table
            ref="xTable"
            resizable
            row-id="id"
            :data="tableData"
            :tree-config="{transform: true, rowField: 'id', parentField: 'parentId', line: true}"
            :checkbox-config="{labelField: 'name', checkRowKeys: ['122000', '20000']}"
    >
        <ta-big-table-column type="checkbox" title="Sex" width="400" tree-node />
        <ta-big-table-column field="size" title="Size" />
        <ta-big-table-column field="type" title="Type" />
        <ta-big-table-column field="date" title="Date" />
    </ta-big-table>
</template>
<script >
    export default {
        data () {
            return {
                tableData: [],
            }
        },
        created () {
            this.tableData = mockTreeData
        },
    }
</script>
```
