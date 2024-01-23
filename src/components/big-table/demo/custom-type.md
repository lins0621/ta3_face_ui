<cn>
#### 自定义type属性
- `ta-big-table`可以自定义`type`属性
- `type`传入一个自定义类型,并实现`type`的渲染方法,就可以实现自己需要的`type`类型
</cn>

<us>
#### custom type
extra type
</us>

```html

<template>
    <div>
        <h3>通过ta-big-table-column标签传入type属性</h3>
        <ta-big-table highlight-hover-row height="400" :data="tableData">
            <ta-big-table-column type="checkbox" width="60"/>
            <ta-big-table-column :type="customType" field="date" title="自定义type类型的日期列"/>
            <ta-big-table-column field="date" title="日期"/>
        </ta-big-table>
        <h3>通过columns属性传入type属性</h3>
        <ta-big-table highlight-hover-row height="400" :data="tableData" :columns="tableColumns"/>
    </div>
</template>
<script>
    import moment from 'moment'


    export default {
        data() {
            const tableColumns = [
                {
                    type: {
                        type: 'checkbox',
                    },
                    width: '60',
                }, {
                    type: {
                        type: 'customType',
                        customRender:this.customRenderStart,
                    },
                    field: 'date',
                    title: '自定义type类型的日期列',
                }, {
                    field: 'date',
                    title: '日期',
                }]
            return {
                loading: false,
                tableData: [],
                tableColumns,
                sexList: [
                    {
                        label: '女',
                        value: '2',
                    },
                    {
                        label: '男',
                        value: '1',
                    }
                ],
                customType: {type: 'custom', customRender: this.customRender,},
            }
        },
        created() {
            this.tableData = [
                {id: 10001, date: '2022-02-02',},
                {id: 10002, date: '2022/12/31',},
                {id: 10003, date: '12/13/2022',},
                {id: 10004, date: '2022.1.2',},
                {id: 10005, date: Date.now(),},
                {id: 10006, date: '2022/1/18 10:05',},
                {id: 10007, date: 'Wed Aug 24 2016 22:26:19 GMT+0800',}
            ]
        },
        methods: {
            customRenderStart(h, v) {
                // jsx语法 
                // return (
                //  <span>{ moment(v).format('YYYYMMDD') }</span>
                // )
                // render函数
                return this.$createElement('span', {}, moment(v).format('YYYYMMDD'))
            },
            
            customRender(h, v) {
                // jsx语法 
                // return (
                //  <span>{ moment(v).format('YYYY^MM^DD') }</span>
                // )
                // render函数
                return this.$createElement('span', {}, moment(v).format('YYYY^MM^DD'))
            },
        },
    }
</script>
<style>
    .custom-yes-or-no-class {
        border-bottom: 0 !important;
    }
</style>

```
