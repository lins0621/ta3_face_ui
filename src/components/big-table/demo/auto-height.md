
<cn>
#### 自适应高度
- ta-big-table通过设置height设置设置表格高度
- ta-big-table设置高度之后会固定表头
- ta-big-table通过设置 height=auto 表格会自动根据父容器的高度去铺满，但是只会在数据重新加载时才会计算
- ta-big-table可以根据不同场景添加 auto-resize（父元素监听），这样就只需要通过样式控制父容器高度就可以实现响应式表格
- height可以设置相对于父容器的百分比
</cn>

<us>
#### auto height
auto height
</us>

```html
<template>
      <div>
           <ta-button @click="tableHeight = '300px'">高300px</ta-button>
            <ta-button @click="tableHeight = '500px'">高500px</ta-button>
            <ta-button @click="tableHeight = '800px'">高800px</ta-button>
        <div :style="{height: tableHeight,marginTop:'10px'}">
          <ta-big-table
            border
            height="auto"
            auto-resize
            :data="tableData">
            <ta-big-table-column type="seq" width="60"></ta-big-table-column>
            <ta-big-table-column field="name" title="Name"></ta-big-table-column>
            <ta-big-table-column field="age" title="Age"></ta-big-table-column>
            <ta-big-table-column field="address" title="Address" show-overflow></ta-big-table-column>
          </ta-big-table>
        </div>
</div>
</template>
<script>
export default {
  data () {
      let da=[];
      for(let i = 0; i < 50;i++){
        da.push({
           name: '名字'+ i,
           age:i,
           address:'地球村'
         })
       }
    return {
     tableHeight:'200px',
      tableData: da
    }
  }
}
</script>
```
