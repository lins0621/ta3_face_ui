<cn>
#### 列宽渲染问题
如果需要将表格放到隐藏的元素中，那么就必然会导致宽度无法计算，例如使用`v-show`控制的隐藏显示，`ta-big-table`已经渲染了，但是处在隐藏状态，解决方法如下：
- 如果是用变量触发的切换显示隐藏状态，则可使用`sync-resize`监听该变量变化，会在`ta-big-table`内部调用`recalculate`计算宽度
- 如果是容器的宽度高度变化导致宽度出现问题，则可使用`auto-resize`属性自动监听父容器来触发重新计算表格
- 如果上述两个方法不生效，或者导致渲染明显出现几秒的卡顿，则在`$nextTick`中主动调用`recalculate`
  ```
  this.$nextTick(() => {
    this.$refs.table.recalculate()
  })
  ```
<span style="color: orange">本例解决的问题是`big-table`已经渲染上去，但是由于是隐藏的，宽度无法计算，所以在显示的时候需要重新计算宽度</span>
</cn>

<us>
#### Column render demo
Column render demo
</us>

```html
<template>
  <div>
    <ta-step :current="step" />
    <ta-big-table
      v-show="step === 1"
      ref="table1"
      border
      highlight-hover-row
      height="400"
      :data="tableData1"
    >
      <ta-big-table-column type="seq" width="60" />
      <ta-big-table-column type="checkbox" title="ID" width="140" />
      <ta-big-table-column field="name" title="Name" sortable />
      <ta-big-table-column field="address" title="Address" show-overflow />
    </ta-big-table>
    <ta-big-table
      v-show="step === 2"
      ref="table1"
      border
      highlight-hover-row
      height="400"
      :data="tableData2"
      :sync-resize="step"
    >
      <ta-big-table-column type="seq" width="60" />
      <ta-big-table-column type="checkbox" title="ID" width="140" />
      <ta-big-table-column field="name" title="Name" sortable />
      <ta-big-table-column field="role" title="Role" show-overflow />
    </ta-big-table>
    <div>
      <ta-button @click="prev">
        prev
      </ta-button>
      <ta-button @click="next">
        next
      </ta-button>
    </div>
  </div>
</template>

<script >
export default {
  data () {
    return {
      step: 1,
      tableData1: [
        { id: 10001, name: 'Test1', role: 'Develop', sex: '1', age: 28, address: 'ta-big-table 从入门到放弃', },
        { id: 10002, name: 'Test2', role: 'Test', sex: '2', age: 22, address: 'Guangzhou', },
        { id: 10003, name: 'Test3', role: 'PM', sex: '1', age: 32, address: 'Shanghai', },
        { id: 10004, name: 'Test4', role: 'Designer', sex: '2', age: 23, address: 'ta-big-table 从入门到放弃', },
        { id: 10005, name: 'Test5', role: 'Develop', sex: '1', age: 30, address: 'Shanghai', },
        { id: 10006, name: 'Test6', role: 'Designer', sex: '2', age: 21, address: 'ta-big-table 从入门到放弃', },
        { id: 10007, name: 'Test7', role: 'Test', sex: '1', age: 29, address: 'ta-big-table 从入门到放弃', },
        { id: 10008, name: 'Test8', role: 'Develop', sex: '2', age: 35, address: 'ta-big-table 从入门到放弃', }
      ],
      tableData2: [
        { id: 10001, name: 'Test1', role: 'Develop', sex: '1', age: 28, address: 'ta-big-table 从入门到放弃', },
        { id: 10002, name: 'Test2', role: 'Test', sex: '2', age: 22, address: 'Guangzhou', },
        { id: 10003, name: 'Test3', role: 'PM', sex: '1', age: 32, address: 'Shanghai', },
        { id: 10004, name: 'Test4', role: 'Designer', sex: '2', age: 23, address: 'ta-big-table 从入门到放弃', },
        { id: 10005, name: 'Test5', role: 'Develop', sex: '1', age: 30, address: 'Shanghai', },
        { id: 10006, name: 'Test6', role: 'Designer', sex: '2', age: 21, address: 'ta-big-table 从入门到放弃', },
        { id: 10007, name: 'Test7', role: 'Test', sex: '1', age: 29, address: 'ta-big-table 从入门到放弃', },
        { id: 10008, name: 'Test8', role: 'Develop', sex: '2', age: 35, address: 'ta-big-table 从入门到放弃', }
      ],
    }
  },
  methods: {
    next(){
      this.step < 2 && this.step++
    },
    prev(){
      this.step > 1 && this.step--
    },
  },
}
</script>

```
