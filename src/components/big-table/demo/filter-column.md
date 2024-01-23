<cn>
#### 过滤
- ta-big-table通过使用ta-big-table-column-filter组件进行筛选
- ta-big-table-column-filter使用filterType属性指定类型,类型有input/select/number/tree/date/collection
- ta-big-table-column-filter使用filterProps对指定的组件进行传参，例如filterType为tree,则应该传treeData参数
- ta-big-table-column-filter使用filterMethod可以用来自定义过滤方法，一般情况下不用传，复杂情况下可以自己设置
- 使用ta-big-table-column-filter方式配置筛选,在筛选后默认会在表格头部出现筛选情况，可以使用showHeaderFilter属性将其关闭
- 使用ta-big-table-column-filter方式配置筛选,不需要在column上面设置filters等属性
- 如果ta-big-table-column-filter方式配置筛选的过滤方式不符合要求，可以使用-自定义过滤，请查看自定义过滤例子
</cn>

<us>
#### filter
filter
</us>

```html
<template>
    <div>
        <div style="margin-bottom: 10px">
            <ta-button @click="filterNameEvent">
                筛选 Name
            </ta-button>
            <ta-button @click="addAgeOneFilter">
                新增Age一个6~7的条件
            </ta-button>
            <ta-button @click="deleteAgeOneSixSevenFilter([{data: 6},{data: 7}])">
                删除Age一个6~7的过滤条件
            </ta-button>
            <ta-button @click="$refs.xTable.clearFilter($refs.xTable.getColumnByField('age'))">
                清除 Age 的所有筛选条件
            </ta-button>
            <ta-button @click="$refs.xTable.clearFilter()">
                清除所有的筛选条件
            </ta-button>
        </div>
        <ta-big-table
                ref="xTable"
                border
                highlight-hover-row
                height="400"
                :loading="loading"
                :data="tableData"
                :tree-config="{children: 'children'}"
        >
            <ta-big-table-column type="seq" width="60" />
            <ta-big-table-column
                    field="name"
                    title="Name"
                    sortable
            >
                <ta-big-table-column-filter :filter-props="{placeholder: '请输入名字进行过滤'}" />
            </ta-big-table-column>

            <ta-big-table-column
                    field="role"
                    title="Role"
                    sortable
            >
                <ta-big-table-column-filter
                        :filter-props="{treeData: treeData,treeCheckStrictly:false,}"
                        :filter-multiple="true"
                        filter-type="tree"
                />
            </ta-big-table-column>
            <ta-big-table-column
                    field="sex"
                    title="Sex"
                    collection-type="SEX"
                    sortable
            >
                <ta-big-table-column-filter filter-type="collection" collection-type="sex" />
                <!--                或者字典也可以如下写法-->
                <!--        <ta-big-table-column-filter
                          :filter-props="{collectionType: 'sex'}"
                          filter-type="select"
                        />-->
            </ta-big-table-column>
            <ta-big-table-column field="age" title="Age">
                <ta-big-table-column-filter filter-type="number" />
            </ta-big-table-column>
            <ta-big-table-column field="age1" title="Age自定义">
                <ta-big-table-column-filter
                        filter-type="number"
                        :filters-start-props="{placeholder:' 输入第一个数'}"
                        :filters-end-props="{placeholder: '输入第二个数'}"
                        :filter-method="filterAge"
                />
            </ta-big-table-column>
            <ta-big-table-column field="time" title="Time" sortable>
                <ta-big-table-column-filter filter-type="date" />
            </ta-big-table-column>
            <ta-big-table-column field="open" title="状态">
                <ta-big-table-column-filter filter-type="select" :filter-props="{options: options}" />
                <template #default="{row}">
                    <span>{{ row.open === '1' ? '开启' : '关闭' }}</span>
                </template>
            </ta-big-table-column>
        </ta-big-table>
    </div>
</template>
<script>
    const treeData = [
        {
            label: '程序狗1',
            value: '程序狗1',
            children: [
                {
                    label: '程序狗2',
                    value: '程序狗2',
                    children: [
                        {
                            label: '程序狗3',
                            value: '程序狗3',
                            children: [
                                { label: '程序狗4', value: '程序狗4', }
                            ],
                        }
                    ],
                }
            ],
        },
        { label: '程序狗10', value: '程序狗10', },
        { label: '程序狗11', value: '程序狗11', }
    ]
    export default {
        data () {
            return {
                treeData: treeData,
                loading: false,
                tableData: [],
                options: [
                    { label: '关闭', value: '0', },
                    { label: '开启', value: '1', }
                ],
            }
        },
        created () {
            // 异步加载数据
            this.findList()
        },
        methods: {
            /**
             * 用户自定义的methods过滤方法
             * @param value
             * @param option
             * @param row
             * @param column
             * @returns {boolean}
             */
            filterAge ({ value, option, row, column, }) {
                const { filters, } = column
                const data = row[column.property]
                if (data === '' || isNaN(Number(data))) return false // 不是数字类型，过滤不通过
                // 将filters变成二维数组
                const handleArr = this.arrayTwoDimensionalArray(filters.filter(i => i.checked))
                const length = handleArr.length
                for (let i = 0; i < length; i++) {
                    const filters = handleArr[i]
                    const minV = filters[0].data
                    const maxV = filters.length === 2 ? filters[1].data : ''
                    if ((minV === undefined || minV === '') && maxV) {
                        // 只输入了右边值
                        if (Number(data) <= Number(maxV)) return true
                    } else if ((maxV === undefined || maxV === '') && minV) {
                        // 只输入了左边值
                        if (Number(data) >= Number(minV)) return true
                    } else if ((minV === undefined || minV === '') && (maxV === undefined || maxV === '')) {
                        // 俩都不输入
                        return true
                    } else {
                        // 输入了俩值
                        if (minV <= Number(data) && Number(data) <= maxV) return true
                    }
                }
                return false
            },
            deleteNameOneFilter (index) {
                const xTable = this.$refs.xTable
                const column = xTable.getColumnByField('name')
                const { filters, } = column
                filters.splice(index, 1)
                // 修改条件之后，需要手动调用 updateData 处理表格数据
                xTable.updateData()
            },
            deleteAgeOneSixSevenFilter (arr) {
                const xTable = this.$refs.xTable
                const column = xTable.getColumnByField('age')
                const { filters, } = column
                const index = filters.findIndex((item, i, filterArr) => {
                    return Number(item.data) === Number(arr[0].data) && Number(filterArr[i + 1].data) === Number(arr[1].data)
                })
                if (index !== -1) {
                    filters.splice(index, 2)
                    // 修改条件之后，需要手动调用 updateData 处理表格数据
                    xTable.updateData()
                }
            },
            addAgeOneFilter () {
                const xTable = this.$refs.xTable
                const column = xTable.getColumnByField('age')
                const { filters, } = column
                const addFilters = [{
                    label: '6',
                    value: '6',
                    data: '6',
                    checked: true,
                    _checked: true,
                }, {
                    label: '7',
                    value: '7',
                    data: '7',
                    checked: true,
                    _checked: true,
                }]
                // 如果此过滤条件还没存在才能添加，存在了就不再添加
                if (!this.judgeHas(addFilters)) filters.push(...addFilters)
                // 修改条件之后，需要手动调用 updateData 处理表格数据
                xTable.updateData()
            },
            /**
             * 判断是否已经存在
             * @param filterArr
             * @returns {boolean}
             */
            judgeHas (filterArr) { // 判断过滤条件是否已经存在
                const xTable = this.$refs.xTable
                const column = xTable.getColumnByField('age')
                const { filters, } = column
                let has = false
                const handleArr = this.arrayTwoDimensionalArray(filters.filter(i => i.checked))
                for (let i = 0; i < handleArr.length; i++) {
                    const group = handleArr[i]
                    if (group.length === 2) {
                        const first = this._handleNumberValue(group[0].data || group[0].value) === this._handleNumberValue(filterArr[0].data || filterArr[0].value)
                        const second = this._handleNumberValue(group[1].data || group[1].value) === this._handleNumberValue(filterArr[1].data || filterArr[1].value)
                        if (first && second) {
                            has = true
                            return has
                        }
                    }
                }
            },
            /**
             * 处理数字工具方法
             * @param value
             * @returns {string|number}
             * @private
             */
            _handleNumberValue (value) {
                if (value === '') {
                    return ''
                } else {
                    return Number(value)
                }
            },
            findList () {
                const list = []
                for (let i = 0; i < 50; i++) {
                    list.push({
                        name: '王' + i + '狗',
                        role: '程序狗' + i,
                        sex: i % 2 === 1 ? '1' : '2',
                        age: i === 0 || i > 40 ? '' : i-2 + '',
                        age1: i === 0 || i > 40 ? '' : i + '',
                        time: i > 29 ? '--' : `2022-04-${i > 9 ? i > 29 ? '' : i : '0' + i}`,
                        open: i % 2 + '',
                    })
                }
                this.loading = true
                return new Promise(resolve => {
                    setTimeout(() => {
                        this.tableData = list
                        this.loading = false
                        resolve()
                    }, 300)
                })
            },
            filterNameEvent () {
                const xTable = this.$refs.xTable
                const column = xTable.getColumnByField('name')
                const { filters, } = column
                const filterData = {
                    label: '1',
                    value: '1',
                    data: '1',
                    checked: true,
                }
                const has = filters.findIndex(item => {
                    return item.value === filterData.value
                })
                if (has > -1) {
                    // 修改
                    filters.splice(has,1,filterData)
                } else {
                    // 添加一个筛选项条件
                    filters.push(filterData)
                }
                // 修改条件之后，需要手动调用 updateData 处理表格数据
                xTable.updateData()
            },
            filterAgeEvent () {
                const xTable = this.$refs.xTable
                const column = xTable.getColumnByField('age')
                const minValue = {
                    label: '3',
                    value: 3,
                    data: 5,
                    checked: true,
                }
                const maxValue = {
                    label: '5',
                    value: 5,
                    data: 5,
                    checked: true,
                }
                column.filters.push(minValue, maxValue)
                // 修改条件之后，需要手动调用 updateData 处理表格数据
                xTable.updateData()
            },
            // 处理数组的工具方法
            arrayTwoDimensionalArray (arr) {
                const resultArr = [] // 声明数组
                arr.forEach((item, index) => {
                    const page = Math.floor(index / 2) // 计算该元素为第几个素组内
                    if (!resultArr[page]) { // 判断是否存在
                        resultArr[page] = []
                    }
                    resultArr[page].push(item)
                })
                return resultArr
            },
        },
    }
</script>
```
