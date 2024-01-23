
<cn>
#### 自定义过滤
- ta-big-table-column通过设置 filters 属性和 filter-method 方法可以开启列筛选功能，通过 filter-multiple=false 设置为单选
- 如果是服务端筛选，只需在`ta-big-table`标签上添加 `:filter-config='{remote: true}'` 和 `filter-change` 事件就可以实现
- 如果是动态数据请通过 setFilter 方法更新，参数 filters 不支持动态数据
- $panel 对象为自定义筛选:
    - changeOption(event, checked, option) 更新选项的状态
    - confirmFilter() 确认筛选
    - resetFilter() 清除筛选条件
</cn>

<us>
#### custom filter
custom filter
</us>

```html
<template>
    <div>
        <div style="margin-bottom: 10px">
            <ta-button @click="filterNameEvent">
                筛选 Name
            </ta-button>
            <ta-button @click="filterAgeEvent">
                筛选 Age
            </ta-button>
            <ta-button @click="updateNameFilterEvent">
                更改 Name 的筛选条件
            </ta-button>
            <ta-button @click="$refs.xTable.clearFilter($refs.xTable.getColumnByField('age'))">
                清除 Age 的筛选条件
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
        >
            <ta-big-table-column type="seq" width="60" />
            <ta-big-table-column
                    field="name"
                    title="Name"
                    sortable
                    :filters="[{ label: '包含3', value: '3' }]"
                    :filter-method="filterNameMethod"
                    :filterRecoverMethod="filterNameRecoverMethod"
            />
            <ta-big-table-column
                    field="role"
                    title="Role"
                    sortable
                    :filters="[{ data: '' }]"
                    :filter-method="filterRoleMethod"
            >
                <template #filter="{ $panel, column }">
                    <ta-select v-for="(option, index) in column.filters" :key="index" v-model="option.data" :get-popup-container="setPopupContainer" style="margin: 10px;width:120px;" @change="$panel.changeOption($event, !!option.data, option)">
                        <ta-select-option v-for="(label, cIndex) in roleList" :key="cIndex" :value="label">
                            {{ label }}
                        </ta-select-option>
                    </ta-select>
                </template>
            </ta-big-table-column>
            <ta-big-table-column
                    field="sex"
                    title="Sex"
                    sortable
                    :filter-multiple="false"
                    :filters="[{label: '男', value:'1'}, {label: '女', value: ''}]"
            />
            <ta-big-table-column field="age" title="Age" :filters="[{ data: '' }]" :filterRecoverMethod="filterAgeRecoverMethod" :filter-method="filterAgeMethod">
                <template #filter="{ $panel, column }">
                    <template v-for="(option, index) in column.filters">
                        <ta-input :key="index" v-model="option.data" style="margin: 10px;width:120px;" placeholder="按回车确认筛选" @change="$panel.changeOption($event, !!option.data, option)" @keyup.enter="$panel.confirmFilter()" />
                    </template>
                </template>
            </ta-big-table-column>
            <ta-big-table-column field="depart" title="部门"  :filter-multiple="false" :filters="[{data: ''}]" :filter-method="departFilteMethod">
                <!--        多选的输入框此类情况可以用显示头部筛选情况，给table 添加 :show-header-filter="true"-->
                <template #filter="{$panel,column}">
                    <ta-input
                            @keyup.enter="(event) => filterInputFilter(event.target.value,column,$panel)"
                    />
                </template>
            </ta-big-table-column>
            <ta-big-table-column field="time" title="Time" sortable />
        </ta-big-table>
    </div>
</template>
<script>

    export default {
        data () {
            return {
                loading: false,
                tableData: [],
                roleList: ['程序狗1', '程序狗2', '程序狗3'],
            }
        },
        created () {
            // 异步加载数据
            this.findList()
        },
        methods: {
            // 自定义重置方法，设置filters
            filterNameRecoverMethod(filters) {
                filters?.forEach(filter => {
                    filter.checked = false
                    filter._checked = false
                })
            },
            // 自定义重置方法，设置filters
            filterAgeRecoverMethod(filters) {
                filters[0].data = 3
                filters[0].checked = true
                filters[0]._checked = true
            },
            departFilteMethod ({ value, option, row, column, }) {
                const filterList = []
                let show = false
                column.filters.forEach(item => {
                    if (item.checked) {
                        filterList.push(item.data)
                    }
                })
                for (let i = 0; i < filterList.length; i++) {
                    if (row.depart.indexOf(filterList[i]) > -1) {
                        show = true
                        break
                    }
                }
                return show
            },
            filterInputFilter (value, column,$panel) {
                const { filters, } = column
                filters.push({
                    label: value,
                    value: value,
                    data: value,
                    checked: true,
                    _checked: true,
                })
                $panel.confirmFilter()
            },
            setPopupContainer (trigger) {
                return trigger.parentNode
            },
            findList () {
                const list = []
                for (let i = 0; i < 50; i++) {
                    list.push({
                        name: '王' + i + '狗',
                        role: '程序狗' + i,
                        sex: i % 2 + '',
                        age: i,
                        depart: '部门' + i,
                        time: i,
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
            filterNameMethod ({ value, row, column, }) {
                // 姓名筛选 筛选包含选定值的
                return row.name.indexOf(value) > -1
            },
            filterRoleMethod ({ option, row, }) {
                // 角色筛选 筛选选中值和目标值相同的
                return row.role === option.data
            },
            filterAgeMethod ({ option, row, }) {
                //  年龄筛选 筛选 年龄大于输入值的
                return row.age > Number(option.data)
            },
            updateNameFilterEvent () {
                const xTable = this.$refs.xTable
                const column = xTable.getColumnByField('name')
                // 修改筛选列表，并默认设置为选中状态
                xTable.setFilter(column, [
                    { label: '包含 1', value: '1', },
                    { label: '包含 2', value: '2', },
                    { label: '包含 4', value: '4', checked: true, },
                    { label: '包含 5', value: '5', },
                    { label: '包含 6', value: '6', }
                ])
                // 修改条件之后，需要手动调用 updateData 处理表格数据
                xTable.updateData()
            },
            filterNameEvent () {
                const xTable = this.$refs.xTable
                const column = xTable.getColumnByField('name')
                // 修改第二个选项为勾选状态
                const option = column.filters[0]
                option.checked = true
                // 修改条件之后，需要手动调用 updateData 处理表格数据
                xTable.updateData()
            },
            filterAgeEvent () {
                const xTable = this.$refs.xTable
                const column = xTable.getColumnByField('age')
                // 修改第一个选项为勾选状态
                const option = column.filters[0]
                option.data = '26'
                option.checked = true
                // 修改条件之后，需要手动调用 updateData 处理表格数据
                xTable.updateData()
            },
        },
    }
</script>

```
