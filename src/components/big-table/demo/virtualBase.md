<cn>
#### 虚拟滚动
ta-big-table可通过`height`或`max-height`设置的值触发规则自动启用虚拟渲染
- 默认情况下，如果设置了`height`或`max-height`则会根据触发规则自动启用虚拟渲染，触发规则由`scroll-x.gt` | `scroll-y.gt` 关闭或设置。虚拟滚动启用后只会渲染指定范围内的可视区数据，其他的数据将被卷去收起，当滚动到可视区时才被渲染出来
- 手动调优，对于低性能的浏览器可以通过设置`oSize`偏移量来缓解渲染次数，偏移量越大渲染次数就越少，但是每次渲染的耗时就越久，通过指定`scroll-x={gt: 20}`或`scroll-y={gt: 40}`适合的参数可以手动调优，如果为 `0` 则总是启用，如果为 `-1` 关闭虚拟滚动
- `height`可以设置固定高度，亦可以设置成`auto`或者`100%`进行自适应
- 通过设置 `max-height` 启用最大高度，当数据少时自适应，当数据超过最大高度时自动显示滚动条
</cn>

<us>
#### virtual
virtual
</us>

```html
<template>
  <div>
    <ta-big-table
      border
      show-overflow
      highlight-hover-row
      height="300"
      :sort-config="{trigger: 'cell'}"
      :data="tableData"
    >
      <ta-big-table-column type="seq" width="100" />
      <ta-big-table-column field="name" title="Name" sortable />
      <ta-big-table-column field="sex" title="Sex" />
      <ta-big-table-column field="age" title="Age" />
      <ta-big-table-column field="address" title="Address" show-overflow />
    </ta-big-table>
  </div>
</template>

<script >
const data = Array.from({length: 5000, }).map((item, index) => ({
  name: 'test' + index,
  sex: index,
  age: index,
  address: index,
}))

export default {
  data () {
    return {
      tableData: data,
    }
  },
}
</script>

```
