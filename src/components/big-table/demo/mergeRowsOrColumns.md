<cn>
#### 合并行列
- ta-big-table在多行或多列共用一个数据时，可以合并行或列。
- ta-big-table传入`span-method`方法可以实现合并行或列，方法的参数是一个对象，里面包含当前行`row`、当前列`column`、当前行号`rowIndex`、当前列号`columnIndex`四个属性。该函数可以返回一个包含两个元素的数组，第一个元素代表`rowspan`，第二个元素代表`colspan`。 也可以返回一个键名为`rowspan`和`colspan`的对象。
</cn>

<us>
#### mergeRowsOrColumns
mergeRowsOrColumns
</us>

```html
<template>
  <div>
   <p class="fenge" style="color: red">合并列</p>
    <ta-big-table
      :data="tableData"
      :span-method="arraySpanMethod"
      border
      style="width: 100%">
      <ta-big-table-column
        field="id"
        title="ID"
        width="180">
      </ta-big-table-column>
      <ta-big-table-column
        field="name"
        title="姓名">
      </ta-big-table-column>
      <ta-big-table-column
        field="amount1"
        sortable
        title="数值 1">
      </ta-big-table-column>
      <ta-big-table-column
        field="amount2"
        sortable
        title="数值 2">
      </ta-big-table-column>
      <ta-big-table-column
        field="amount3"
        sortable
        title="数值 3">
      </ta-big-table-column>
    </ta-big-table>
    <p class="fenge" style="color: red">合并行</p>
    <ta-big-table
      :data="tableData"
      :span-method="objectSpanMethod"
      border
      style="width: 100%; margin-top: 20px">
      <ta-big-table-column
        field="id"
        title="ID"
        width="180">
      </ta-big-table-column>
      <ta-big-table-column
        field="name"
        title="姓名">
      </ta-big-table-column>
      <ta-big-table-column
        field="amount1"
        title="数值 1（元）">
      </ta-big-table-column>
      <ta-big-table-column
        field="amount2"
        title="数值 2（元）">
      </ta-big-table-column>
      <ta-big-table-column
        field="amount3"
        title="数值 3（元）">
      </ta-big-table-column>
    </ta-big-table>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        tableData: [{
          id: '12987122',
          name: '王小虎',
          amount1: '234',
          amount2: '3.2',
          amount3: 10
        }, {
          id: '12987123',
          name: '王小虎',
          amount1: '165',
          amount2: '4.43',
          amount3: 12
        }, {
          id: '12987124',
          name: '王小虎',
          amount1: '324',
          amount2: '1.9',
          amount3: 9
        }, {
          id: '12987125',
          name: '王小虎',
          amount1: '621',
          amount2: '2.2',
          amount3: 17
        }, {
          id: '12987126',
          name: '王小虎',
          amount1: '539',
          amount2: '4.1',
          amount3: 15
        }]
      };
    },
    methods: {
      arraySpanMethod({ row, column, rowIndex, columnIndex }) {
        if (rowIndex % 2 === 0) {
          if (columnIndex === 0) {
            return { rowspan: 1, colspan: 2 }
          } else if (columnIndex === 1) {
            return { rowspan: 0, colspan: 0 };
          }
        }
      },

      objectSpanMethod({ row, column, rowIndex, columnIndex }) {
        if (columnIndex === 0) {
          if (rowIndex % 2 === 0) {
            return {
              rowspan: 2,
              colspan: 1
            };
          } else {
            return {
              rowspan: 0,
              colspan: 0
            };
          }
        }
      }
    }
  };
</script>
```
