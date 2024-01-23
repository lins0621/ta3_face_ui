<cn>
#### 虚拟滚动渲染问题
由于组件库中容器组件在第一次渲染的时候`ta-big-table`的`dom`并没有挂载，当`visible`为`true`或者可视的时候，`dom`才进行挂载并且容器的宽度高度可能会变化，导致`ta-big-table`需要重新自适应高度，从而导致卡顿<br>
本例总结了普遍的容器渲染卡顿问题的demo，首先使用`$nextTick`保证能获取到`ref`，其次将`loadData`的第二个参数设置为`true`<br>
<span style="color: orange">本例解决的问题是`ta-big-table`还没有渲染上去，当可视触发渲染的时候，容器出现宽度高度变化导致列表重新渲染多次造成卡顿</span>
</cn>

<us>
#### tab switch
tab switch
</us>

```html
<template>
  <div style="height: 400px">
    <ta-button @click="click1">
      打开modal->table
    </ta-button>
    <ta-button @click="click2">
      打开modal->tabs->table
    </ta-button>
    <ta-button @click="click3">
      打开drawer->table
    </ta-button>
    <ta-tabs class="fit" @change="change">
      <ta-tab-pane key="1" tab="Tab 1" class="fit">
        <ta-big-table
          ref="xTable1"
          border
          show-overflow
          highlight-hover-row
          height="100%"
          :sort-config="{trigger: 'cell'}"
        >
          <ta-big-table-column type="seq" width="100" />
          <ta-big-table-column field="name" title="Name" sortable />
          <ta-big-table-column field="sex" title="Sex" />
          <ta-big-table-column field="age" title="Age" />
          <ta-big-table-column field="address" title="Address" show-overflow />
        </ta-big-table>
      </ta-tab-pane>
      <ta-tab-pane key="2" tab="Tab 2" class="fit">
        <ta-big-table
          ref="xTable2"
          border
          show-overflow
          highlight-hover-row
          height="100%"
          :sort-config="{trigger: 'cell'}"
        >
          <ta-big-table-column type="seq" width="100" />
          <ta-big-table-column field="address" title="Address" show-overflow />
          <ta-big-table-column field="age" title="Age" />
          <ta-big-table-column field="sex" title="Sex" />
          <ta-big-table-column field="name" title="Name" sortable />
        </ta-big-table>
      </ta-tab-pane>
    </ta-tabs>

    <ta-modal v-model="visible1" :body-style="{height: '400px'}" title="test">
      <ta-big-table
        ref="xTable3"
        border
        show-overflow
        highlight-hover-row
        height="100%"
        :sort-config="{trigger: 'cell'}"
      >
        <ta-big-table-column type="seq" width="100" />
        <ta-big-table-column field="address" title="Address" show-overflow />
        <ta-big-table-column field="age" title="Age" />
        <ta-big-table-column field="sex" title="Sex" />
        <ta-big-table-column field="name" title="Name" sortable />
      </ta-big-table>
    </ta-modal>

    <ta-modal v-model="visible2" :body-style="{height: '400px'}" title="test">
      <ta-tabs class="fit" @change="change">
        <ta-tab-pane key="4" tab="Tab 1" class="fit">
          <ta-big-table
            ref="xTable4"
            border
            show-overflow
            highlight-hover-row
            height="100%"
            :sort-config="{trigger: 'cell'}"
          >
            <ta-big-table-column type="seq" width="100" />
            <ta-big-table-column field="name" title="Name" sortable />
            <ta-big-table-column field="sex" title="Sex" />
            <ta-big-table-column field="age" title="Age" />
            <ta-big-table-column field="address" title="Address" show-overflow />
          </ta-big-table>
        </ta-tab-pane>
        <ta-tab-pane key="5" tab="Tab 2" class="fit">
          <ta-big-table
            ref="xTable5"
            border
            show-overflow
            highlight-hover-row
            height="100%"
            :sort-config="{trigger: 'cell'}"
          >
            <ta-big-table-column type="seq" width="100" />
            <ta-big-table-column field="address" title="Address" show-overflow />
            <ta-big-table-column field="age" title="Age" />
            <ta-big-table-column field="sex" title="Sex" />
            <ta-big-table-column field="name" title="Name" sortable />
          </ta-big-table>
        </ta-tab-pane>
      </ta-tabs>
    </ta-modal>
    <ta-drawer :visible="visible3" title="test" :width="500" @close="visible3 = false">
      <ta-big-table
        ref="xTable6"
        border
        show-overflow
        highlight-hover-row
        height="100%"
        :sort-config="{trigger: 'cell'}"
      >
        <ta-big-table-column type="seq" width="100" />
        <ta-big-table-column field="address" title="Address" show-overflow />
        <ta-big-table-column field="age" title="Age" />
        <ta-big-table-column field="sex" title="Sex" />
        <ta-big-table-column field="name" title="Name" sortable />
      </ta-big-table>
    </ta-drawer>
  </div>
</template>

<script>
const data = Array.from({length: 5000, }).map((item, index) => ({
  name: 'test' + index,
  sex: index,
  age: index,
  address: index,
}))

export default {
  data(){
    return {
      visible1: false,
      visible2: false,
      visible3: false,
    }
  },
  mounted() {
    this.$refs.xTable1.loadData(data, true)
  },
  methods: {
    change(activeKey){
      this.$nextTick(() => {
        this.$refs[`xTable${activeKey}`].loadData(data, true)
      })
    },
    click1() {
      this.visible1 = !this.visible1
      if(this.visible1){
        this.$nextTick(() => {
          this.$refs.xTable3.loadData(data, true)
        })
      }
    },
    click2() {
      this.visible2 = !this.visible2
      if(this.visible2){
        this.$nextTick(() => {
          this.$refs.xTable4.loadData(data, true)
        })
      }
    },
    click3() {
      this.visible3 = !this.visible3
      if(this.visible3){
        this.$nextTick(() => {
            this.$refs.xTable6.loadData(data, true)
        })
      }
    },
  },
}
</script>

```
