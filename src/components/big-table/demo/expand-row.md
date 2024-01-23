
<cn>
#### 展开行
- ta-big-table通过设置expand-config 属性和big-table-column的type=expand 开启行展开功能,通过 big-table-column的slot 可以配置行展开显示的具体内容
- ta-big-table通过配置expand-config的 expandRowKeys 参数设置默认展开行，指定默认值big-table需要有 row-id属性
- ta-big-table通过配置expand-config的 expandAll 参数设置默认展开所有行
- ta-big-table通过配置expand-config的labelField 设置显示在展开行上的属性
- ta-big-table通过配置expand-config={accordion:true} 属性来开启同一级的节点，每次只能展开一个,实现手风琴展开效果
- ta-big-table通过配置expand-config={iconOpen:'xxx', iconClose:'xxx'} 局部替换默认的图标
</cn>

<us>
#### expand row
expand row
</us>

```html
<template>
  <div style="height:400px">
        <ta-big-table
          ref="xTable"
          border
          height="auto"
          :data="tableData"
          row-id="id"
          :expand-config="{expandRowKeys:[10001],labelField:'name'}"
          @toggle-row-expand="toggleExpandChangeEvent">
           <template #topBar>
            <ta-button @click="$refs.xTable.toggleRowExpand(tableData[1])">切换第二行展开</ta-button>
            <ta-button @click="$refs.xTable.setRowExpand([tableData[2], tableData[3]], true)">设置第三、四行展开</ta-button>
            <ta-button @click="$refs.xTable.setAllRowExpand(true)">设置所有行展开</ta-button>
            <ta-button @click="$refs.xTable.clearRowExpand()">关闭所有行展开</ta-button>
          </template>
          <ta-big-table-column type="seq" width="60"></ta-big-table-column>
          <ta-big-table-column type="expand" width="120" >
            <template v-slot:content="{ row, rowIndex }">
                <ta-descriptions title="User Info">
                  <ta-descriptions-item label="ID">
                    {{ row.id }}
                  </ta-descriptions-item>
                  <ta-descriptions-item label="Name">
                   {{ row.name }}
                  </ta-descriptions-item>
                  <ta-descriptions-item label="Age">
                    {{row.age}}
                  </ta-descriptions-item>
                  <ta-descriptions-item label="Sex">
                    {{CollectionLabel('SEX',row.sex)}}
                  </ta-descriptions-item>
                  <ta-descriptions-item label="Address">
                   {{row.address}}
                  </ta-descriptions-item>
                </ta-descriptions>
            </template>
          </ta-big-table-column>
          <ta-big-table-column field="name" title="Name"></ta-big-table-column>
          <ta-big-table-column field="sex" title="Sex" collection-type="SEX"></ta-big-table-column>
          <ta-big-table-column field="age" title="Age"></ta-big-table-column>
          <ta-big-table-column field="address" title="address"></ta-big-table-column>
        </ta-big-table>
  </div>
</template>
<script>
        export default {
          data () {
            return {
              tableData: [
                    { id: 10001, name: 'Test1', role: 'Develop', sex: '1', age: 28, address: 'ta-big-table 从入门到放弃' },
                    { id: 10002, name: 'Test2', role: 'Test', sex: '2', age: 22, address: 'Guangzhou' },
                    { id: 10003, name: 'Test3', role: 'PM', sex: '1', age: 32, address: 'Shanghai' },
                    { id: 10004, name: 'Test4', role: 'Designer', sex: '2', age: 23, address: 'ta-big-table 从入门到放弃' },
                    { id: 10005, name: 'Test5', role: 'Develop', sex: '1', age: 30, address: 'Shanghai' },
                    { id: 10006, name: 'Test6', role: 'Designer', sex: '2', age: 21, address: 'ta-big-table 从入门到放弃' },
                    { id: 10007, name: 'Test7', role: 'Test', sex: '1', age: 29, address: 'ta-big-table 从入门到放弃' },
                    { id: 10008, name: 'Test8', role: 'Develop', sex: '2', age: 35, address: 'ta-big-table 从入门到放弃' }
               ]
            }
          },
          methods: {
            toggleExpandChangeEvent ({ row, expanded }) {
              message.info('行展开事件' + expanded)
            }
          }
        }
</script>
```
