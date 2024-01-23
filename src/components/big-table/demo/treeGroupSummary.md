<cn>
#### 树形表格分组合计
- ta-big-table树形表格分组合计示例
</cn>

<us>
#### Tree table group summary
Tree table group summary
</us>

```html

<template>
    <div>
        <div style="margin-bottom: 20px">
            <ta-button @click="$refs.xTable.setAllTreeExpand(true)">展开全部</ta-button>
            <ta-button @click="$refs.xTable.setAllTreeExpand(false)">收起全部</ta-button>
        </div>
        <ta-big-table
                resizable
                show-footer
                ref="xTable"
                max-height="400"
                :loading="loading"
                :tree-config="tableTreeConfig"
                :span-method="colspanMethod"
                :footer-method="footerMethod"
                :data="tableData">
            <ta-big-table-column field="name" title="名称" tree-node :formatter="formatName"></ta-big-table-column>
            <ta-big-table-column field="level" title="级别"></ta-big-table-column>
            <ta-big-table-column field="age" title="年龄"></ta-big-table-column>
            <ta-big-table-column field="rate" title="分数"></ta-big-table-column>
        </ta-big-table>
    </div>
</template>
<script >
    import TaUtils from '@yh/ta-utils'

    export default {
        data() {
            return {
                loading: false,
                tableData: [],
                tableTreeConfig: {
                    children: 'children',
                    expandAll: false // 默认是否全部展开
                }
            }
        },
        created() {
            this.loading = true
            this.findList().then(data => {
                this.tableData = this.getGroupSummary(data)
                this.loading = false
            })
        },
        methods: {
            findList() {
                return new Promise(resolve => {
                    setTimeout(() => {
                        let list = [
                            {
                                name: '一班',
                                level: '',
                                age: '',
                                rate: '',
                                children: [
                                    {
                                        name: 'test7',
                                        rate: 9,
                                        age: 24,
                                        level: 1
                                    },
                                    {
                                        name: 'test6',
                                        rate: 14,
                                        age: 20,
                                        level: 3
                                    },
                                    {
                                        name: '第一组',
                                        level: '',
                                        age: '',
                                        rate: '',
                                        children: [
                                            {
                                                name: 'test85',
                                                rate: 13,
                                                age: 32,
                                                level: 1
                                            },
                                            {
                                                name: 'test37',
                                                rate: 9,
                                                age: 29,
                                                level: 4
                                            },
                                            {
                                                name: 'test93',
                                                rate: 22,
                                                age: 28,
                                                level: 5
                                            },
                                            {
                                                name: 'test90',
                                                rate: 55,
                                                age: 26,
                                                level: 2
                                            }
                                        ]
                                    },
                                    {
                                        name: 'test32',
                                        rate: 11,
                                        age: 21,
                                        level: 1
                                    }
                                ]
                            },
                            {
                                name: '二班',
                                level: '',
                                age: '',
                                rate: '',
                                children: [
                                    {
                                        name: 'test15',
                                        rate: 13,
                                        age: 32,
                                        level: 1
                                    },
                                    {
                                        name: 'test44',
                                        rate: 9,
                                        age: 29,
                                        level: 4
                                    },
                                    {
                                        name: '第一组',
                                        level: '',
                                        age: '',
                                        rate: '',
                                        children: [
                                            {
                                                name: 'test37',
                                                rate: 9,
                                                age: 29,
                                                level: 4
                                            },
                                            {
                                                name: 'test93',
                                                rate: 22,
                                                age: 28,
                                                level: 5
                                            }
                                        ]
                                    },
                                    {
                                        name: '第二组',
                                        level: '',
                                        age: '',
                                        rate: '',
                                        children: [
                                            {
                                                name: 'test74',
                                                rate: 11,
                                                age: 32,
                                                level: 5
                                            },
                                            {
                                                name: 'test99',
                                                rate: 23,
                                                age: 18,
                                                level: 4
                                            },
                                            {
                                                name: '第一排',
                                                level: '',
                                                age: '',
                                                rate: '',
                                                children: [
                                                    {
                                                        name: 'test48',
                                                        rate: 77,
                                                        age: 29,
                                                        level: 4
                                                    },
                                                    {
                                                        name: 'test38',
                                                        rate: 34,
                                                        age: 21,
                                                        level: 2
                                                    }
                                                ]
                                            },
                                            {
                                                name: 'test16',
                                                rate: 22,
                                                age: 26,
                                                level: 5
                                            }
                                        ]
                                    },
                                    {
                                        name: 'test91',
                                        rate: 16,
                                        age: 27,
                                        level: 5
                                    },
                                    {
                                        name: '第三组',
                                        level: '',
                                        age: '',
                                        rate: '',
                                        children: [
                                            {
                                                name: 'test77',
                                                rate: 11,
                                                age: 35,
                                                level: 1
                                            },
                                            {
                                                name: 'test89',
                                                rate: 40,
                                                age: 18,
                                                level: 4
                                            },
                                            {
                                                name: 'test10',
                                                rate: 22,
                                                age: 20,
                                                level: 2
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                name: '三班',
                                level: '',
                                age: '',
                                rate: '',
                                children: [
                                    {
                                        name: 'test6',
                                        rate: 3,
                                        age: 22,
                                        level: 2
                                    },
                                    {
                                        name: 'test2',
                                        rate: 5,
                                        age: 25,
                                        level: 3
                                    },
                                    {
                                        name: 'test42',
                                        rate: 17,
                                        age: 35,
                                        level: 4
                                    }
                                ]
                            }
                        ]
                        resolve(list)
                    }, 300)
                })
            },
            formatName({row}) {
                return row.children && row.children.length ? `${row.name} (${row.num}人)` : row.name
            },
            // 计算逻辑
            handleSummary(children) {
                return {
                    num: TaUtils.sum(children, 'num'),
                    level: Math.floor(TaUtils.sum(children, 'level')),
                    age: parseInt(TaUtils.mean(children, 'age')),
                    rate: TaUtils.sum(children, 'rate')
                }
            },
            getGroupSummary(data) {
                TaUtils.eachTree(data, (row, index, items, path, parent, nodes) => {
                    let children = row.children
                    if (children && children.length) {
                        // 合计子节点
                        Object.assign(row, this.handleSummary(children))
                    } else {
                        row.num = 1
                        if (index === items.length - 1) {
                            // 全量汇总
                            for (let len = nodes.length - 2; len >= 0; len--) {
                                Object.assign(nodes[len], this.handleSummary(nodes[len].children))
                            }
                        }
                    }
                }, this.tableTreeConfig)
                TaUtils.eachTree(data, (row) => {
                    let children = row.children
                    if (children && children.length) {
                        // 动态增加一行汇总
                        children.push({
                            name: `合计 (${row.name})`,
                            level: row.level,
                            age: row.age,
                            rate: row.rate
                        })
                    }
                }, this.tableTreeConfig)
                return data
            },
            colspanMethod({
                              row,
                              column
                          }) {
                // 当行被展开时将行合并
                let xTree = this.$refs.xTree
                if (row.children && row.children.length && xTree && xTree.isTreeExpandByRow(row)) {
                    if (column.treeNode) {
                        return {
                            rowspan: 1,
                            colspan: 4
                        }
                    } else {
                        return {
                            rowspan: 0,
                            colspan: 0
                        }
                    }
                }
            },
            footerMethod({
                             columns,
                             data
                         }) {
                return [
                    columns.map((column, columnIndex) => {
                        if (columnIndex === 0) {
                            return `合计 (${TaUtils.sum(data, 'num')}人)`
                        }
                        switch (column.property) {
                            case 'level':
                                return `总共 ${Math.floor(TaUtils.sum(data, 'level'))}`
                            case 'age':
                                return `平均年龄 ${parseInt(TaUtils.mean(data, 'age'))}`
                            case 'rate':
                                return `总分 ${TaUtils.sum(data, 'rate')}`
                        }
                        return '-'
                    })
                ]
            }
        }
    }
</script>
```
