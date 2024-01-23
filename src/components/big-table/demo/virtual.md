<cn>
#### 树形表格的虚拟滚动
- ta-big-table树形表格可通过给`tree-config`对象提供`virtual`属性,实现虚拟滚动,注意,需要同时提供表格的`height`属性
</cn>

<us>
#### virtual-tree-table
virtual tree like table
</us>

```html

<template>
    <div>
        <ta-big-table :data="tableData" :tree-config="{children: 'children', virtual: true,}" height="500"
                      show-overflow>
            <ta-big-table-column field='name' title="Name" width="280" tree-node></ta-big-table-column>
            <ta-big-table-column field="size" title="Size"></ta-big-table-column>
            <ta-big-table-column field="type" title="Type"></ta-big-table-column>
        </ta-big-table>
    </div>
</template>
<script>
    const mockTreeData = [{
        id: '30000',
        parentId: null,
        name: '文件夹 30000',
        size: '3k',
        type: '',
        date: '2019-05-14',
        childCols: [],
        childData: [],
        checked: false,
        indeterminate: false,
        children: []
    }, {
        id: '40000',
        parentId: null,
        name: '文件夹 40000',
        size: '3k',
        type: '',
        date: '2019-05-14',
        childCols: [],
        childData: [],
        checked: false,
        indeterminate: false,
    }]
    // for (let i = 0; i < 1000; i++) {
    //   mockTreeData.push({
    //     id: i+6+'0000',
    //     parentId: null,
    //     name: 'ta-big-table 测试数据 10000',
    //     size: '53k',
    //     type: '',
    //     date: '2019-10-22',
    //     checked: false,
    //     indeterminate: false,
    //     childCols: [],
    //     childData: [],
    //   })
    // }
    for (let i = 0; i < 1000; i++) {
        mockTreeData[0].children.push({
            id: '1' + i + 3 + '000',
            parentId: null,
            name: 'ta-big-table 测试数据 10000' + i + 3,
            size: '53k',
            type: '',
            date: '2019-10-22',
            checked: false,
            indeterminate: false,
            childCols: [],
            childData: [],
        })
    }
    export default {
        data() {
            return {
                tableData: mockTreeData,
            }
        }
    }
</script>

```
