
<cn>
#### 自定义模板
- ta-big-table使用 slot 自定义模板；可以实现自定义任意内容及 html 元素
    - default：自定义内容模板（提前格式化（最优） > formatter（field值发生变化时） > slots（即时））
    - header：自定义表头模板
    - footer：自定义表尾模板
    - filter：自定义筛选模板（建议使用渲染器，可以更好的复用）
    - edit：自定义可编辑模板（建议使用渲染器，可以更好的复用）
    - topBar: 自定义页头 (可用于放表格批量操作按钮)
    - bottomBar: 自定义页尾 (可用于放表格分页条)
</cn>

<us>
#### custom template
custom template
</us>

```html
<template>

<div style="height: 600px">
        <ta-big-table
          border
          resizable
          show-footer
          ref="xTable"
          height="auto"
          :footer-method="footerMethod"
          :data="tableData"
          @checkbox-change="checkboxChangeEvent"
          @checkbox-all="checkboxChangeEvent">
          <template v-slot:topBar>
               <ta-button>新增</ta-button>
               <ta-dropdown>
                 <ta-menu slot="overlay">
                   <ta-menu-item key="1">删除</ta-menu-item>
                   <ta-menu-item key="2">保存</ta-menu-item>
                 </ta-menu>
                 <ta-button style="margin-left: 8px">
                   操作 <ta-icon type="down" />
                 </ta-button>
               </ta-dropdown>
          </template>

          <ta-big-table-column type="checkbox" width="60"></ta-big-table-column>
          <ta-big-table-column type="seq" width="160" :resizable="false" show-overflow>
            <template v-slot:header>
              <div class="first-col">
                <div class="first-col-top">名称</div>
                <div class="first-col-bottom">序号</div>
              </div>
            </template>
            <template v-slot:footer="{ items, _columnIndex }">
              <ta-button type="primary" @click="clickFooterItem(items, _columnIndex)" size="small">支持</ta-button>
              <ta-button @click="clickFooterItem(items, _columnIndex)" size="small">放弃</ta-button>
            </template>
            <template v-slot="{ row }">
              <ta-button @click="showDetailEvent(row)">弹框{{ row.name }}</ta-button>
            </template>
          </ta-big-table-column>
          <ta-big-table-column field="name" title="链接" sortable>
            <template v-slot="{ row }">
              <a href="" target="_black">我是超链接：{{ row.name }}</a>
            </template>
          </ta-big-table-column>
          <ta-big-table-column field="sex" title="app.body.label.sex" :filters="[{data: ''}]" :filter-method="filterSexMethod">
            <template v-slot:header>
              <span style="color: red;">自定义头部</span>
            </template>
            <template v-slot:footer="{ items, _columnIndex }">
              <span style="color: red">累计：{{ items[_columnIndex] }}</span>
            </template>
            <template v-slot:filter="{ $panel, column }">
              <template v-for="(option, index) in column.filters">
                <ta-input style="width:120px" class="my-filter" type="type" v-model="option.data" :key="index" @change="changeFilterEvent($event, option, $panel)"/>
              </template>
            </template>
            <template v-slot="{ row }">
              <span>{{ row.sex }} </span>
              <ta-button size="small" type="link">编辑</ta-button>
              <ta-button size="small" type="link">删除</ta-button>
            </template>
          </ta-big-table-column>
          <ta-big-table-column field="time" title="Time">
            <template v-slot:header>
              <ta-input v-model="value1" placeholder="放个输入框" size="small"></ta-input>
            </template>
            <template v-slot="{ row, rowIndex }">
              <template v-if="rowIndex === 2">
                <ta-switch v-model="row.flag"></ta-switch>
              </template>
              <template v-else-if="rowIndex === 3">
                <ta-switch v-model="row.flag" on-label="开" off-label="关"></ta-switch>
              </template>
              <template v-else>
                <span>{{ formatDate(row.time) }}</span>
              </template>
            </template>
          </ta-big-table-column>
          <ta-big-table-column field="address" title="Address" show-overflow>
            <template v-slot="{ row, rowIndex }">
              <template v-if="rowIndex === 1">
                <select v-model="row.flag1" >
                  <option value="Y" label="是"></option>
                  <option value="N" label="否"></option>
                </select>
              </template>
              <template v-else>
                <a href="">{{ row.name }}</a>
              </template>
            </template>
          </ta-big-table-column>
          <ta-big-table-column field="html1" title="Html片段" width="200" show-overflow>
            <template v-slot="{ row }">
              <span v-html="row.html1"></span>
            </template>
            <template v-slot:footer>
              <span>
                <img src="./img1.gif" style="width: 36px;">自定义模板<img src="./img1.gif" style="width: 30px;">
              </span>
            </template>
          </ta-big-table-column>
        <template v-slot:bottomBar>
            <ta-pagination></ta-pagination>
          </template>
        </ta-big-table>
        <ta-modal v-model="showDetails" title="查看详情" width="800" height="400" @ok="close" @cancel="close">
          <template v-slot>{{ selectRow ? selectRow.name : '' }}</template>
        </ta-modal>
       </div>
</template>
<script>
 export default {
          data () {
            return {
              value1: '',
              value2: '',
              showDetails: false,
              selectRow: null,
              isAllChecked: false,
              isIndeterminate: false,
              selectRecords: [],
              tableData: [
                { id: 10001, name: 'Test1', role: 'Develop', sex: 'Man', age: 28, address: 'ta-big-table 从入门到放弃', flag: false, time: 1600261774531, html1: '<span style="color:red">ta-big-table从入门到废弃</span>',  },
                { id: 10002, name: 'Test2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou', flag: false, time: 1600261774531, html1: '',},
                { id: 10003, name: 'Test3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai', flag: true, time: 1600261774531, html1: '<span style="color:orange">ta-big-table从入门到废弃</span>',  },
                { id: 10004, name: 'Test4', role: 'Designer', sex: 'Women ', age: 23, address: 'ta-big-table 从入门到放弃', flag: false, time: 1600261774531, html1: '', },
                { id: 10005, name: 'Test5', role: 'Develop', sex: 'Women ', age: 30, address: 'Shanghai', flag: true, time: 1600261774531, html1: '', },
                { id: 10006, name: 'Test6', role: 'Designer', sex: 'Women ', age: 21, address: 'ta-big-table 从入门到放弃', flag: true, time: 1600261774531, html1: '<span style="color:blue">ta-big-table从入门到废弃</span>',  },
                { id: 10007, name: 'Test7', role: 'Test', sex: 'Man ', age: 29, address: 'ta-big-table 从入门到放弃', flag: false, time: 1600261774531, html1: '',  },
                { id: 10008, name: 'Test8', role: 'Develop', sex: 'Man ', age: 35, address: 'ta-big-table 从入门到放弃', flag: false, time: 1600261774531, html1: '', }
              ],

            }
          },
          methods: {
            close () {
              this.showDetails = false
            },
            formatDate (value) {
              // return TaUtils.toDateString(value, 'yyyy-MM-dd HH:mm:ss.S')
              return value
            },
            filterSexMethod ({ option, row }) {
              return row.sex === option.data
            },
            changeFilterEvent (evnt, option, $panel) {
              $panel.changeOption(evnt, !!option.data, option)
            },
            showDetailEvent (row) {
              this.selectRow = row
              this.showDetails = true
            },
            clickFooterItem (items, _columnIndex) {
              message.info(`点击了表尾第${_columnIndex}列`)
            },
            checkboxChangeEvent ({ records }) {
              this.isAllChecked = this.$refs.xTable.isAllCheckboxChecked()
              this.isIndeterminate = this.$refs.xTable.isCheckboxIndeterminate()
              this.selectRecords = records
            },
            changeAllEvent () {
              this.$refs.xTable.setAllCheckboxRow(this.isAllChecked)
              this.selectRecords = this.$refs.xTable.getCheckboxRecords()
            },
            footerMethod ({ columns, data }) {
              return [
                columns.map(column => {
                  if (['sex', 'num'].includes(column.property)) {
                    // return TaUtils.sum(data, column.property)
                    return 111
                  }
                  return null
                })
              ]
            }
          }
        }

</script>
<style>
    .first-col {
          position: relative;
          height: 20px;
        }
        .first-col:before {
          content: "";
          position: absolute;
          left: -15px;
          top: 10px;
          width: 170px;
          height: 1px;
          transform: rotate(20deg);
          background-color: #e8eaec;
        }
        .first-col .first-col-top {
          position: absolute;
          right: 4px;
          top: -10px;
        }
        .first-col .first-col-bottom {
          position: absolute;
          left: 4px;
          bottom: -10px;
        }
        .my-filter {
          margin: 10px;
        }
        .page-left {
          position: absolute;
          left: 10px;
          top: 50%;
          transform: translateY(-50%);
          z-index: 10;
        }
</style>
```
