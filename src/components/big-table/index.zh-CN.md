## API

### 基本属性

| 属性 | 说明 | 类型 | 可选值 | 默认值 |
|---|---|---|---|---|
| id | <div style="width: 280px">唯一标识（被某些特定的功能所依赖）</div> | String | | |
| data | 表格数据（与 loadData 行为一致，更新数据是不会重置状态） | Array | | |
| columns | 如果是通过数组数据来生成表格列，则使用此属性 | Array\<{ 列的API属性，参考 table-column或table-colgroup的属性}\> | - | - |
| height | 表格的高度；支持铺满父容器或者固定高度，如果设置 auto 为铺满父容器（如果设置为 auto，则必须确保存在父节点且不允许存在相邻元素,如果设置为固定高度,那么这个表格将会使用虚拟滚动以优化性能）;从`@yh/ta404-ui@1.5.129`开始,由于`auto-resize`的默认值调整为`true`, 此时如果`height`设置为`auto`或`100%`时,需要确保其父容器(以及父容器的父容器直到`body`层级)有`height`,否则会出现`ResizeObserver loop limit exceeded`错误 | Number, String | auto, %, px | |
| max-height | 表格的最大高度 | Number, String | %, px | |
| auto-resize | 自动监听父元素的变化去重新计算表格（对于父元素可能存在动态变化、显示隐藏的容器中、列宽异常等场景中的可能会用到） | Boolean | | TRUE |
| sync-resize | 自动跟随某个属性的变化去重新计算表格，和手动调用 recalculate 方法是一样的效果（对于通过某个属性来控制显示/隐藏切换时可能会用到） | Boolean, String, Number | | |
| resizable | 所有的列是否允许拖动列宽调整大小 | Boolean | | 默认 false，继承 setup.table.resizable |
| stripe | 是否带有斑马纹（需要注意的是，在可编辑表格场景下，临时插入的数据不会有斑马纹样式） | Boolean | | 默认 false，继承 setup.table.stripe |
| border | 是否带有边框 | Boolean, String | default（默认）, full（完整边框）, outer（外边框）, inner（内边框）, none（无边框） | 默认 false，继承 setup.table.border |
| round | 是否为圆角边框 | Boolean | | 默认 false，继承 setup.table.round |
| size | 表格的尺寸 | String | medium, small, mini | 继承上下文 |
| loading | 表格是否显示加载中 | Boolean | | TRUE |
| align | 所有的列对齐方式 | String | left（左对齐）, center（居中对齐）, right（右对齐） | left |
| header-align | 所有的表头列的对齐方式 | String | left（左对齐）, center（居中对齐）, right（右对齐） | 继承 align |
| footer-align | 所有的表尾列的对齐方式 | String | left（左对齐）, center（居中对齐）, right（右对齐） | 继承 align |
| show-header | 是否显示表头 | Boolean | | FALSE |
| highlight-current-row | 是否要高亮当前行 | Boolean | | FALSE |
| highlight-hover-row | 鼠标移到行是否要高亮显示 | Boolean | | FALSE |
| highlight-current-column | 是否要高亮当前列 | Boolean | | FALSE |
| highlight-hover-column | 鼠标移到列是否要高亮显示 | Boolean | | FALSE |
| highlight-cell | 只对 edit-config 配置时有效，是否在编辑时高亮单元格边框（只支持部分） | Boolean | | FALSE |
| row-class-name | 给行附加 className | String, Function | | |
| cell-class-name | 给单元格附加 className | String, Function | | |
| header-row-class-name | 给表头的行附加 className | String, Function | | |
| header-cell-class-name | 给表头的单元格附加 className | String, Function | | |
| footer-row-class-name | 给表尾的行附加 className | String, Function | | |
| footer-cell-class-name | 给表尾的单元格附加 className | String, Function | | |
| cell-style | 给单元格附加样式 | Object, Function | | |
| header-cell-style | 给表头单元格附加样式 | Object, Function | | |
| footer-cell-style | 给表尾单元格附加样式 | Object, Function | | |
| row-style | 给行附加样式，也可以是函数 | Object, Function | | |
| header-row-style | 给表头行附加样式 | Object, Function | | |
| footer-row-style | 给表尾行附加样式 | Object, Function | | |
| show-footer | 是否显示表尾 | Boolean | | FALSE |
| footer-method | 表尾的数据获取方法，返回一个二维数组 | Function | | |
| merge-cells | 临时合并指定的单元格（不能用于树形结构、展开行，不建议用于固定列） | Array\<{ row: number, col: number, rowspan: number, colspan: number }\> | | |
| merge-footer-items | 临时合并表尾（不能用于树形结构、展开行,不建议用于固定列） | Array\<{ row: number, col: number, rowspan: number, colspan: number }\> | | |
| span-method | 自定义合并函数，返回计算后的值，不能用于虚拟滚动、树形结构、展开行、固定列 | Object | | { rowspan: 1, colspan: 1} |
| footer-span-method | 表尾合并行或列，返回计算后的值，不能用于虚拟滚动、树形结构、展开行、固定列 | Object | | { rowspan: 1, colspan: 1} |
| show-overflow | 设置所有内容过长时显示为省略号（如果是固定列建议设置该值，提升渲染速度） | Boolean, String | ellipsis（只显示省略号）,title（并且显示为原生 title）,tooltip（并且显示为 tooltip 提示） | |
| show-header-overflow | 设置表头所有内容过长时显示为省略号 | Boolean, String | ellipsis（只显示省略号）,title（并且显示为原生 title）,tooltip（并且显示为 tooltip 提示） | |
| show-footer-overflow | 设置表尾所有内容过长时显示为省略号 | Boolean, String | ellipsis（只显示省略号）,title（并且显示为原生 title）,tooltip（并且显示为 tooltip 提示） | |
| column-key | 是否需要为每一列的 VNode 设置 key 属性（非特殊情况下不需要使用） | Boolean | | FALSE |
| row-key | 是否需要为每一行的 VNode 设置 key 属性（非特殊情况下没必要设置） | Boolean | | FALSE |
| row-id | 自定义行数据唯一主键的字段名（行数据必须要有唯一主键，默认自动生成） | String | | 默认 _XID，继承 setup.table.rowId |
| keep-source | 保持原始值的状态，被某些功能所依赖，比如编辑状态、还原数据等（开启后影响性能，具体取决于数据量） | Boolean | | 默认 false，继承 setup.table.keepSource |
| z-index | 自定义堆叠顺序（对于某些特殊场景，比如被遮挡时可能会用到） | Number | | 继承 setup.table.zIndex |
| animat | 表格动画效果开关（关闭后视觉效果更快） | Object | | 默认 true，继承 setup.table.animat |
| cloak | 用于低性能的浏览器，可以设置为 true 来避免初始化渲染时的闪动 | Boolean | | 默认 false，继承 setup.table.cloak |
| delay-hover | 当表格发生拖动、滚动...等行为时，至少多少毫秒之后才允许触发 hover 事件 | Number | | 默认 250，继承 setup.table.delayHover |
| params | 额外的参数（可以用来存放一些私有参数） | Object | | |
| control-column | 列控制(可以进行列显示隐藏和列拖拽排序)，具体使用看[上面示例](process.env.VUE_APP_PUBLIC_PATH/components/big-table-cn/#components-big-table-demo-columns-control) | Object, Boolean | | |
| draggable | 表格行是否可以拖拽, 属性的配置请参考[示例](#components-big-table-demo-data-line-draggable)  | object\|Boolean | false | |

### 列配置

column-config 列的默认参数
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
width | 列的默认宽度 | Number, String | auto, px, % |
min-width | 列的默认最小宽度 | Number, String | auto, px, % |
### 列属性

table-column属性
属性 | 说明 | 类型 | 可选值 | 默认值 | 版本
---|---|---|---|---|---|
type | 列的类型 | string\|object | seq(index), checkbox(selection), radio, expand, html, yesOrNo, date, operate, | undefined | yesOrNo和date类型从1.5.128起支持,operate从1.5.136支持
field | 列字段名（注：属性层级越深，渲染性能就越差，例如：aa.bb.cc.dd.ee） | String | |
title | 列标题（支持开启国际化） | String | |
width | 列宽度（如果为空则均匀分配剩余宽度，如果全部列固定了，可能会存在宽屏下不会铺满，可以配合 "%" 或者 "min-width"布局） | Number, String | px, % | 继承 table.column-config.width
min-width | 最小列宽度；会自动将剩余空间按比例分配 | Number, String | px, % | 继承 table.column-config.minWidth
resizable | 列是否允许拖动列宽调整大小 | Boolean | | 继承 table.resizable
visible | 列是否显示 | Boolean | |
fixed | 将列固定在左侧或者右侧（注意：固定列应该放在左右两侧的位置） | String | left（固定左侧）, right（固定右侧） |
align | 列对齐方式 | String | left（左对齐）, center（居中对齐）, right（右对齐） | 继承 table.align
header-align | 表头列的对齐方式 | String | left（左对齐）, center（居中对齐）, right（右对齐） | 继承 align \> 继承 table.header-align
footer-align | 表尾列的对齐方式 | String | left（左对齐）, center（居中对齐）, right（右对齐） | 继承 align \> 继承 table.footer-align
show-overflow | 当内容过长时显示为省略号 | String,Boolean | ellipsis（只显示省略号）, title（并且显示为原生 title）, tooltip（并且显示为 tooltip 提示） | 继承 table.show-overflow
show-header-overflow | 当表头内容过长时显示为省略号 | String,Boolean | ellipsis（只显示省略号）, title（并且显示为原生 title）, tooltip（并且显示为 tooltip 提示） | 继承 table.show-header-overflow
show-footer-overflow | 当表尾内容过长时显示为省略号 | Boolean, String | ellipsis（只显示省略号）,title（并且显示为原生 title）,tooltip（并且显示为 tooltip 提示） | 继承 table.show-footer-overflow
class-name | 给单元格附加 className | String, Function | |
header-class-name | 给表头的单元格附加 className | String, Function | |
footer-class-name | 给表尾的单元格附加 className | String, Function | |
formatter | 格式化显示内容 | Function, Array, String | |
seq-method | 只对 type=seq 有效，自定义索引方法 | Function | |
sortable | 是否允许列排序 | Boolean | | FALSE
sort-by | 只对 sortable 有效，自定义排序的属性 | string | |
sort-method | 只对 sortable 有效，列的排序方法，该方法的返回值用来决定该行的排序规则 | Function | |
remote-sort | 是否使用服务端排序，如果设置为 true 则不会对数据进行处理 | Boolean | | 继承 table.remote-sort
showHeaderFilter | 是否将过滤情况显示在表头(如果使用了taTableColumnFilter组件则默认显示) | Boolean | |
filters | 配置筛选条件（注：筛选只能用于列表，如果是树结构则过滤根节点） | Array | |
filters.label | 显示的值 | String | |
filters.value | 实际的值 | Any | |
filters.checked | 默认是否选中 | Boolean | | FALSE
filters.resetValue | 重置时的默认值 | Any | |
filters.data | 自定义渲染的数据值（当使用自定义模板时可能会用到） | Any | |
filter-multiple | 只对 filters 有效，筛选是否允许多选 | Boolean | | TRUE
filter-method | 只对 filters 有效，列的筛选方法，该方法的返回值用来决定该行是否显示 | Function | |
filterRecoverMethod | 自定义筛选时，重置的自定义方法 | Function(filters,column): void | - |
filter-render | 筛选渲染器配置项 | Object | |
filter-render.name | 渲染器名称 | String | input, textarea, select, $input, $textarea, $select |
filter-render.props | 渲染的参数（请查看目标渲染的 Props） | Object | |
filter-render.attrs | 渲染的属性（请查看目标渲染的 Attribute） | Object | |
filter-render.events | 渲染组件的事件（请查看目标渲染的 Events） | Object | | {row,rowIndex,$rowIndex,column,columnIndex,$columnIndex}, ...[目标渲染的 arguments]
filter-render.nativeEvents | 渲染组件的原生事件（请查看目标渲染的 Events） | Object | | {row,rowIndex,$rowIndex,column,columnIndex,$columnIndex}, ...[目标渲染的 arguments]
export-method | 自定义单元格数据导出方法，该方法 Function({ row, column }) 的返回值将会被导出 | Function | |
footer-export-method | 自定义表尾单元格数据导出方法，该方法 Function({ items, _columnIndex }) 的返回值将会被导出 | Function | |
title-help | 标题帮助图标配置项 | any | |
title-help.message | 提示消息（支持开启国际化） | string | |
title-help.icon | 自定义图标 | string | |
cell-type | 只对特定功能有效，单元格值类型（例如：导出数据类型设置） | String | auto（默认自动转换），number（数值）, string（字符串） | auto
cell-render | 默认的渲染器配置项 | Object | |
cell-render.name | 渲染器名称 | String | input, textarea, select, $input, $select, $button, $buttons, $switch |
cell-render.props | 渲染的参数（请查看目标渲染的 Props） | Object | |
cell-render.attrs | 渲染的属性（请查看目标渲染的 Attribute） | Object | |
cell-render.events | 渲染组件的事件（请查看目标渲染的 Events） | Object | | {row,rowIndex,$rowIndex,column,columnIndex,$columnIndex}, ...[目标渲染的 arguments]
cell-render.nativeEvents | 渲染组件的原生事件（请查看目标渲染的 Events） | Object | | {row,rowIndex,$rowIndex,column,columnIndex,$columnIndex}, ...[目标渲染的 arguments]
cell-render.content | 渲染组件的内容（仅用于特殊组件） | String | |
edit-render | 可编辑渲染器配置项 | Object | |
edit-render.name | 渲染器名称 | String | input, textarea, select, $input, $input-number, $select, $date-picker, $time-picker, $week-picker, $month-picker, $quarter-picker, $year-picker, $range-picker, $rate, $switch, $checkbox, $radio, $cascader, $tree-select |
edit-render.props | 渲染的参数（请查看目标渲染的 Props） | Object | |
edit-render.style | style样式 | String, Object | |
edit-render.class | class类 | String, Array, Object | |
edit-render.attrs | 渲染的属性（请查看目标渲染的 Attribute） | Object | |
edit-render.events | 渲染组件的事件（请查看目标渲染的 Events） | Object | | {row,rowIndex,$rowIndex,column,columnIndex,$columnIndex}, ...[目标渲染的 arguments]
edit-render.autofocus | 如果是自定义渲染可以指定聚焦的选择器，例如 .my-input | String | |
edit-render.renderCell | 自定义渲染 | Function | (h,renderOpt,{cellValue,}) => string |
edit-render.nativeEvents | 渲染组件的原生事件（请查看目标渲染的 Events） | Object | | {row,rowIndex,$rowIndex,column,columnIndex,$columnIndex}, ...[目标渲染的 arguments]
content-render | 内容渲染配置项 | Object | |
content-render.name | 渲染器名称 | String | input, textarea, select, $input, $textarea, $select |
content-render.props | 渲染的参数（请查看目标渲染的 Props） | Object | |
content-render.attrs | 渲染的属性（请查看目标渲染的 Attribute） | Object | |
content-render.events | 渲染组件的事件（请查看目标渲染的 Events） | Object | | {data, property}, ...[目标渲染的 arguments]
content-render.nativeEvents | 渲染组件的原生事件（请查看目标渲染的 Events） | Object | | {data, property}, ...[目标渲染的 arguments]
tree-node | 只对 tree-config 配置时有效，指定为树节点 | Boolean | | FALSE
params | 额外的参数（可以用来存放一些私有参数） | Object | |
col-id | 自定义列的唯一主键（注：非必要不需要设置，操作不正确将导致出现问题） | string | number | |
format | 当`type`为`date`时,可通过此属性快速设置日期格式,这个值会被对象形式的`type`中的`format`覆盖 | string | undefined | 1.5.136 |
operate | 当`type`为`operate`时,传递给`ta-table-operate`的属性,这个值会被对象形式的`type`中的`operate`覆盖 | Array | undefined | 1.5.136 |

**注意:**

- `type`可以配置为`object`,例如`type='checkbox`可以配置为`:type='{type: "checkbox"}'`, 一般不需要再提供额外的参数即可正常渲染
- `type`为`yesOrNo`时,**必须**同时在列的属性上提供`field`属性.当其配置为`object`时,提供下列参数进行自定义

```
{
 type: 'yesOrNo',
 // 自定义tag的样式
 customStyle:'',
 // 自定义tag的class
 customClass:'',
 // 自定义当customFlag返回true时显示的值
 customYes:'是',
 // 自定义当customFlag返回false时显示的值
 customNo:'否',
 // 自定义判断值是否
 customFlag(v){
 return (value === '1' || value === 'true')
 },
 // 完全自定义yesOrNo的渲染
 // 注意: 使用此自定义函数后,上面的几个自定义属性都不再有效
 // 需要自行处理相关的值
 // 支持jsx语法或通过h函数自行构建
 customRender(h, cellValue, row, column){
 // return (
 // <span>
 // {cellValue}
 // </span>
 // )
 return h('span', {}, [cellValue])
 },
}
```

- `type`为`date`时,**必须**同时在列的属性上提供`field`属性.当其配置为`object`时,提供下列参数进行自定义

```
{
 type: 'date',
 // 自定义显示在表格中的日期的格式
 format:'YYYY-MM-DD', // 默认值为'YYYY-MM-DD'
 // 完全自定义date的渲染
 // 使用此自定义函数后, 上面的属性都将失效
 // 需要自行在此函数中进行定义
 // 支持jsx语法或通过h函数自行构建
 customRender(h, cellValue, row, column){
 const formattedDate = moment(cellValue).format('YYYY-MM-DD')
 // return (
 // <span>{ formattedDate }</span>
 // )
 return h('span', {}, [formattedDate])
 },
}
```

- 当`type`为`operate`时,**必须**同时在列的属性上提供`operate`属性,并在其中传入`operateMenu`定义(
  如果有需要可以同时传入`ta-table-operate`的其他属性).当其配置为`object`时,可以提供下列参数进行自定义

```
{
 type: 'operate',
 // operate-menu的属性
 operate:{
 operateMenu: [],
 // 其他operate-menu的属性
 },
 // 完全自定义operate-menu的渲染
 // 使用此自定义函数后, 上面的属性都将失效
 // 需要自行在此函数中进行定义
 // 支持jsx语法或通过h函数自行构建
 // 可以通过此属性使用自己封装的操作列组件
 customRender(h, cellValue, row, column){
 // return (
 // <span>{ cellValue }</span>
 // )
 return h('span', {}, [cellValue])
 },
}
```

- 当`type`为对象时,你可以完全自定义`type`类型及渲染方法,例如:

```
{
 type: 'custom-type',
 // 自定义类型的渲染方法
 // 支持jsx语法或通过h函数自行构建
 customRender(h, cellValue, row, column){
 const formattedDate = moment(cellValue).format('YYYY-MM-DD')
 // return (
 // <span>{ formattedDate }</span>
 // )
 return h('span', {}, [formattedDate])
 },
}
```
### 列分组属性

table-colgroup属性
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
field | 列字段名（注：属性层级越深，渲染性能就越差，例如：aa.bb.cc.dd.ee） | String | |
title | 列标题（支持开启国际化） | String | |
width | 列宽度（如果为空则均匀分配剩余宽度，如果全部列固定了，可能会存在宽屏下不会铺满，可以配合 "%" 或者 "min-width"布局） |
Number, String | px, % | 继承 table.column-config.width
min-width | 最小列宽度；会自动将剩余空间按比例分配 | Number, String | px, % | 继承 table.column-config.minWidth
resizable | 列是否允许拖动列宽调整大小 | Boolean | | 继承 table.resizable
visible | 列是否显示 | Boolean | |
fixed | 将列固定在左侧或者右侧（注意：固定列应该放在左右两侧的位置） | String | left（固定左侧）, right（固定右侧） |
align | 列对齐方式 | String | left（左对齐）, center（居中对齐）, right（右对齐） | 继承 table.align
header-align | 表头列的对齐方式 | String | left（左对齐）, center（居中对齐）, right（右对齐） | 继承 align \> 继承 table.header-align
show-overflow | 当内容过长时显示为省略号 | String,Boolean | ellipsis（只显示省略号）, title（并且显示为原生 title）, tooltip（并且显示为 tooltip 提示） | 继承 table.show-overflow
show-header-overflow | 当表头内容过长时显示为省略号 | String,Boolean | ellipsis（只显示省略号）, title（并且显示为原生 title）, tooltip（并且显示为 tooltip 提示） | 继承 table.show-header-overflow
header-class-name | 给表头的单元格附加 className | String, Function | |

### 列插槽

名称 | 说明 | 参数
---|---|---
default | 自定义显示内容模板 |<div style="width:340px"> {row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, _columnIndex}</div>
header | 自定义表头内容的模板 | {column, columnIndex, $columnIndex, _columnIndex, $rowIndex}
footer | 自定义表尾内容的模板 | {column, columnIndex, $columnIndex, _columnIndex, $rowIndex, items} v2.8.0
content | 只对 type=expand 有效，自定义展开后的内容模板 | {row, rowIndex, $rowIndex, column} v2.7.0
filter | 只对 filter-render 有效，自定义筛选模板 | {column, columnIndex, $columnIndex}
edit | 只对 edit-render 有效，自定义可编辑组件模板 | {row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, _columnIndex}

### 列过滤

table-column-filter属性
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
filterType | 筛选类型(非必须) | string | input、number、select、collection、date、tree | input
filterMethod | 筛选过滤的方法(非必须) | function | - | -
filterMultiple | 是否多选用于tree和select | boolean | true/false | false
collectionType | 字典类型，只有当type="collection"时再传入 | string | - | -
filterProps | 传递给组件的参数，如select参考ta-select的属性，date参考date-range-picker的属性等 | object | - | -
filterProps.showSum | filterType=select时 是否显示过滤统计 | object | - | -
filtersStartProps | number类型时，第一个input-number框的属性 | object | - | -
filtersEndProps | number类型时，第二个input-number框的属性 | object | - | -



### 列控制配置

control-column | 列控制(可以进行列显示隐藏和列拖拽排序) | Object, Boolean | |
属性 | 说明 | 类型/返回类型 | 可选值 | 默认值
---|---|---|---|---
themeColor | 弹出框的主题色 | String | 颜色值 | 主题色
icon | 表头上方功能图标，可以传入字符串或者一个返回vNode的方法 | String,Function | 图标的type | -
showHiddenConfig | 控制列显示隐藏的配置，传入一个对象，{open\<boolean>,hideInExpand\<boolean>,disabledHiddenColumns<array,function>} 分别为开启和禁止开启关闭的列disabledHiddenColumns为数组时传入列相关的 field或type，hideInExpand 为是否开启隐藏时加入expand中 | Object | - | -
columnSortConfig | 控制拖拽排序的配置，传入一个对象，{{open\<boolean>,onMove\<function>,dragEnd\<function>} 分别为开启，可以在onMove中限制某项不允许排序 | Object | - | -
disabledControlCol | 设置不出现在弹出面板中的列 Function(column) => return boolean,返回true不显示 | Function | - | -
successCallback | 点击确定或者重置的回调 Function({ table, resultColumnsList, type }),返回当前表格，结果表格列，type为重置时传出 | Function | - | -
popperClass | 给弹出的气泡框设置类名，可通过此属性给气泡设置宽高 | String | - | -
hoverShowIcon | 是否鼠标移入表头才出现功能图标 | Boolean | true/false | false
clickOtherClose | 点击气泡框的其它区域关闭，不建议使用 | Boolean | - | false




### 序号配置项

seq-config | 序号配置项 | Object | 继承 setup.table.seqConfig
属性 | 说明 | 类型/返回类型 | 可选值 | 默认值
---|---|---|---|---
startIndex | 设置序号的起始值 | Number | | 0
seqMethod | 自定义序号的方法 Function({ row, rowIndex, column, columnIndex }) 返回处理后的值 | Function | |

### 排序配置项

sort-config | 排序配置项 | Object | 继承 setup.table.sortConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
defaultSort | 默认排序（只会在初始化时被触发一次） | Object | |
defaultSort.field |列字段名 |String| |
defaultSort.order | 排序方式 |String |asc（升序）,desc（降序）, null| |
orders | 自定义轮转顺序 | Array | asc, desc, null | ['asc', 'desc', 'null']
sortMethod | 全局排序方法，当触发排序时会调用该函数 Function({ data, column, property, order }) 返回排序后的列表 | Function | |
remote | 所有列是否使用服务端排序，如果设置为 true 则不会对数据进行处理 | Boolean | |
trigger | 触发方式 | String | default（点击按钮触发）, cell（点击表头触发） | default
showIcon | 是否显示列头排序图标 | Boolean | | TRUE
iconAsc | 自定义升序的图标 | String | |
iconDesc | 自定义降序的图标 | String | |
iconSize | 筛选图标的大小 | String/Number | 14px |

### 筛选配置项

filter-config | 筛选配置项 | Object | | 继承 setup.table.filterConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
remote | 所有列是否使用服务端筛选，如果设置为 true 则不会对数据进行处理 | Boolean | |
filterMethod | 全局筛选方法，当触发筛选时会调用该函数 Function({value, row, column}) 返回是否有效 | Function | |
showIcon | 是否显示列头筛选图标 | Boolean | | TRUE
iconNone | 自定义无条件时显示的图标 | String | |
iconMatch | 自定义带条件时显示的图标 | String | |
iconSize | 过滤图标的大小 | String/Number | 14px |

### 导出配置项

export-config | 导出配置项 | Boolean, Object | | 继承 setup.table.exportConfig
属性 | 说明 | 类型/返回类型 | 可选值 | 默认值
---|---|---|---|---
filename | 文件名 | String | |
sheetName | 表名（只对支持的文档类型有效） | String | |
type | 文件类型 | String | csv, html, xml, txt | csv
types | 可选文件类型列表 | Array | csv, html, xml, txt | ['csv', 'html', 'xml', 'txt']
mode | 输出数据的方式 | String | current, selected, all | current
modes | 输出数据的方式列表 | Array | current, selected, all | ['current', 'selected']
original | 是否为源数据（某些场景下支持 true， 比如虚拟滚动、优化的固定列..，如果需要支持导入，则必须设置为 true） | Boolean | | FALSE
message | 是否显示内置的消息提示 | Boolean | | FALSE
isHeader | 是否需要表头 | Boolean | | TRUE
isFooter | 是否需要表尾 | Boolean | | TRUE
download | 是否马上下载，如果设置为 false 则通过返回结果为内容的 Promise | Boolean | | TRUE
data | 自定义数据 | Array | |
columns | 自定义列（如果指定了 columns 则 columnFilterMethod 默认为空） | Array | |
columnFilterMethod | 列过滤方法，该函数 Function({ column, $columnIndex }) 的返回值用来决定是否过滤掉列 | Function | | 默认过滤掉 type=seq,checkbox,radio 和 field 为空的列
dataFilterMethod | 数据过滤方法，该函数 Function({ row, $rowIndex }) 的返回值用来决定是否过滤掉数据行 | Function | |
footerFilterMethod | 表尾过滤方法，该函数 Function({ items, $rowIndex }) 的返回值用来决定是否过滤掉表尾行 | Function | |
remote | 是否服务端导出 | Boolean | | FALSE
exportMethod | 只对 remote=true 有效，该函数 Function({ options }) 用于自定义导出或服务端导出，返回 Promise | Function | |
style | 只对 type=html 有效，自定义文档的 css 样式信息 | string | |

### 导入配置项

import-config | 导入配置项 | Boolean, Object | | 继承 setup.table.importConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
mode | 导入数据的方式 | String | covering, insert | covering
message | 是否显示内置的消息提示 | Boolean | | FALSE
types | 导入的文件类型列表 | Array | csv, html, xml, txt, xls, xlsx | ['csv', 'html', 'xml', 'txt', 'xls', 'xlsx']
remote | 是否服务端导入 | Boolean | | FALSE
importMethod | 只对 remote=true 有效，该函数 Function({ file, options }) 用于自定义导入或服务端导入，返回 Promise | Function | |

### 打印配置项

print-config | 打印配置项 | Object | | 继承 setup.table.printConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
sheetName | 表名（只对支持的文档类型有效） | String | |
mode | 输出数据的方式 | String | current, selected, all | current
modes | 输出数据的方式列表 | Array | current, selected, all | ['current', 'selected', 'all']
original | 是否为源数据（某些场景下支持 true， 比如虚拟滚动、优化的固定列..，如果需要支持导入，则必须设置为 true） | Boolean | | FALSE
isHeader | 是否需要表头 | Boolean | | TRUE
isFooter | 是否需要表尾 | Boolean | | TRUE
data | 自定义数据 | Array | |
columns | 自定义列（如果指定了 columns 则 columnFilterMethod 默认为空） | Array | |
columnFilterMethod | 列过滤方法，该函数 Function({ column, $columnIndex }) 的返回值用来决定是否过滤掉列 | Function | | 默认过滤掉 type=seq,checkbox,radio 和 field 为空的列
dataFilterMethod | 数据过滤方法，该函数 Function({ row, $rowIndex }) 的返回值用来决定是否过滤掉数据行 | Function | |
footerFilterMethod | 表尾过滤方法，该函数 Function({ items, $rowIndex }) 的返回值用来决定是否过滤掉表尾行 | Function | |
style | 只对 type=html 有效，自定义文档的 css 样式信息 | string | |
content | 自定义打印的内容 | string | |
beforePrintMethod | 该函数 Function({ content, options }) 会在打印之前触发，可以通过返回自定义打印的内容 | ({ content, options }) =\> string | |

### 单选框配置项

radio-config | 单选框配置项 | Object | | 继承 setup.table.radioConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
reserve | 是否保留勾选状态，对于某些场景下非常有用，比如数据被刷新之后还保留之前选中的状态（需要有 row-id） | Boolean | | FALSE
labelField | 单选框显示的字段名，可以直接显示在单选框中 | String | |
checkRowKey | 默认选中开指定行（只会在初始化时被触发一次，需要有 row-id） | Row.rowId | |
checkMethod | 是否允许选中的方法，该方法 Function({row}) 的返回值用来决定这一行的 Radio 是否可以选中 | Function | |
trigger | 触发方式 | String | default（默认）, cell（点击单元格触发）,row（点击行触发） | default
highlight | 高亮选中行 | Boolean | | FALSE

### 复选框配置项

checkbox-config | 复选框配置项 | Object | | 继承 setup.table.checkboxConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
labelField | 复选框显示的字段名，可以直接显示在复选框中 | String | |
checkField | 绑定选中属性，如果设置了该属性渲染速度更快（建议数据量大时使用，行数据中必须存在该字段，否则无效） | String | |
showHeader | 是否显示全选按钮（如果 checkStrictly=true 则默认为 false） | Boolean | | TRUE
checkAll | 默认勾选所有（只会在初始化时被触发一次） | Boolean | | FALSE
checkRowKeys | 默认勾选开指定行（只会在初始化时被触发一次，需要有 row-id） | Array\<Row.rowId\> | |
checkStrictly | 是否严格的遵循父子不互相关联的做法(true严格不关联,false严格关联,`half半关联(上级可控制下级,下级不能控制上级)`) | Boolean /String | | FALSE
isCheckAll | 在checkStrictly和showHeader都为true时,是否支持全选 | Boolean | | FALSE
strict | 严格模式，当数据为空或全部禁用时，列头的复选框为禁用状态 | Boolean | | FALSE
checkMethod | 是否允许勾选的方法，该方法 Function({row}) 的返回值用来决定这一行的 checkbox 是否可以勾选 | Function | |
trigger | 触发方式 | String | default（默认）, cell（点击单元格触发）, row（点击行触发） | default
highlight | 高亮勾选行 | Boolean | | FALSE
reserve | 是否保留勾选状态，对于某些场景可能会用到，比如数据被刷新之后还保留之前选中的状态（需要有 row-id） | Boolean | | FALSE
range | 开启复选框范围选择功能（启用后通过鼠标在复选框的列内滑动选中或取消指定行） | Boolean | | FALSE

### tooltip配置项

tooltip-config | tooltip 配置项 | Object | | 继承 setup.table.tooltipConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
enabled | 所有单元格开启 tooltip 显示 | Boolean | | FALSE
leaveDelay | 鼠标移出后延时多少才隐藏 tooltip | Number | | 300
contentMethod | 该方法 Function({items?, row?, rowIndex?, $rowIndex, column, columnIndex, $columnIndex, type, cell, $event}) 接收一个字符串，可以通过返回值来重写默认的提示内容 | ({items?, row?, rowIndex?, $rowIndex, column, columnIndex, $columnIndex, type, cell, $event}) => String|VNode | |

### 展开行配置项

expand-config | 展开行配置项 | Object | | 继承 setup.table.expandConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
labelField | 展开列显示的字段名，可以直接显示在单元格中 | String | |
expandAll | 默认展开所有行（只会在初始化时被触发一次） | Boolean | | FALSE
expandRowKeys | 默认展开指定行（只会在初始化时被触发一次，需要有 row-id） | Array\<Row.rowId\> | |
accordion | 每次只能展开一行 | Boolean | | FALSE
trigger | 触发方式 | String | default（点击按钮触发）, cell（点击单元格触发）, row（点击行触发） | default
lazy | 是否使用懒加载 | Boolean | | FALSE
loadMethod | 该方法 Function({row, rowIndex?, $rowIndex?}) 用于异步加载展开后的内容（必须返回 Promise\<any[]\> 对象） | Function | |
toggleMethod | 该方法 Function({expanded, column, columnIndex, row, rowIndex?})在展开或关闭触发之前调用，可以通过返回值来决定是否允许继续执行 | Function | |
visibleMethod | 该函数 Function({column, columnIndex, row, rowIndex?}) 的返回值用来决定是否允许显示展开按钮 | Function | |
reserve | 是否保留展开状态，对于某些场景可能会用到，比如数据被刷新之后还保留之前展开的状态（需要有 row-id） | boolean | | FALSE
showIcon | 是否显示图标按钮 | boolean | | TRUE
iconOpen | 自定义展开后显示的图标 | String | |
iconClose | 自定义收起后显示的图标 | String | |
iconLoaded | 自定义懒加载中显示的图标 | String | |

### 树形结构配置项

tree-config | 树形结构配置项 | Boolean, Object | | 继承 setup.table.treeConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
children | 树子节点的属性 | String | | children
indent | 树节点的缩进 | Number | | 20
line | 树节点的连接线（启用连接线会降低渲染性能） | Boolean | | FALSE
expandAll | 默认展开所有子孙树节点（只会在初始化时被触发一次） | Boolean | | FALSE
expandRowKeys | 默认展开指定树节点（只会在初始化时被触发一次，需要有 row-id） | Array\<Row.rowId\> | |
accordion | 对于同一级的节点，每次只能展开一个 | Boolean | | FALSE
trigger | 触发方式 | String | default（点击按钮触发）, cell（点击单元格触发）, row（点击行触发） | default
lazy | 是否使用懒加载（启用后只有指定 hasChild 的节点才允许被点击） | Boolean | | FALSE
hasChild | 只对 lazy 启用后有效，标识是否存在子节点，从而控制是否允许被点击 | String | | hasChild
loadMethod | 该方法 Function({row}) 用于异步加载子节点（必须返回 Promise\<any[]\> 对象） | Function | |
toggleMethod | 该方法 Function({expanded, row, column, columnIndex})在展开或关闭触发之前调用，可以通过返回值来决定是否允许继续执行 | Function | |
reserve | 是否保留展开状态，对于某些场景可能会用到，比如数据被刷新之后还保留之前展开的状态（需要有 row-id） | boolean | | FALSE
showIcon | 是否显示图标按钮 | boolean | | TRUE
iconOpen | 自定义展开后显示的图标 | String | |
iconClose | 自定义收起后显示的图标 | String | |
iconLoaded | 自定义懒加载中显示的图标 | String | |
virtual | 树形表格是否支持虚拟滚动 | boolean | |

### 快捷菜单配置项

menu-config | 快捷菜单配置项 | Object | | 继承 setup.table.menuConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
header | 表头的快捷菜单 | Object | |
header.disabled | 是否禁用右键 | Boolean | | FALSE
header.options | 菜单配置 | Array\<Array\> | |
header.options.code | 菜单键值 | String | |
header.options.name | 菜单名称 | String | |
header.options.prefixIcon | 前缀图标 type \| props | String \| object | |
header.options.suffixIcon | 后缀图标 type \| props | String \| object | |
header.options.className | 菜单项的 className | String | |
header.options.visible | 是否可视 | Boolean | | TRUE
header.options.disabled | 是否禁用 | Boolean | | FALSE
header.options.children | 二级菜单（最多只允许有二级） | Array | |
header.options.children.code | 菜单键值 | String | |
header.options.children.name | 菜单名称 | String | |
header.options.children.prefixIcon | 前缀图标 className | String | |
header.options.children.visible | 是否可视 | Boolean | | TRUE
header.options.children.disabled | 是否禁用 | Boolean | | FALSE
body | 内容的快捷菜单 | Object | |
body.disabled | 是否禁用右键 | Boolean | | FALSE
body.options | 菜单配置 | Array\<Array\> | |
body.options.code | 菜单键值 | String | |
body.options.name | 菜单名称 | String | |
body.options.prefixIcon | 前缀图标 type \| props | String \| object | |
body.options.suffixIcon | 后缀图标 type \| props | String \| object | |
body.options.className | 菜单项的 className | String | |
body.options.visible | 是否可视 | Boolean | | TRUE
body.options.disabled | 是否禁用 | Boolean | | FALSE
body.options.children | 二级菜单（最多只允许有二级） | Array | |
body.options.children.code | 菜单键值 | String | |
body.options.children.name | 菜单名称 | String | |
body.options.children.prefixIcon | 前缀图标 className | String | |
body.options.children.visible | 是否可视 | Boolean | | TRUE
body.options.children.disabled | 是否禁用 | Boolean | | FALSE
footer | 表尾的快捷菜单 | Object | |
footer.disabled | 是否禁用右键 | Boolean | | FALSE
footer.options | 菜单配置 | Array\<Array\> | |
footer.options.code | 菜单键值 | String | |
footer.options.name | 菜单名称（支持开启国际化） | String | |
footer.options.prefixIcon | 前缀图标 type \| props | String \| object | |
footer.options.suffixIcon | 后缀图标 type \| props | String \| object | |
footer.options.className | 菜单项的 className | String | |
footer.options.visible | 是否可视 | Boolean | | TRUE v2.0.20
footer.options.disabled | 是否禁用 | Boolean | | FALSE
footer.options.children | 二级菜单（最多只允许有二级） | Array | |
footer.options.children.code | 菜单键值 | String | |
footer.options.children.name | 菜单名称 | String | |
footer.options.children.prefixIcon | 前缀图标 type \| props | String \| object | |
footer.options.children.visible | 是否可视 | Boolean | | TRUE
footer.options.children.disabled | 是否禁用 | Boolean | | FALSE
trigger | 触发方式 | String | default（默认触发）, cell（右键单元格触发） | default
visibleMethod | 该函数 Function({type, options, columns, row?, rowIndex?, column?, columnIndex?})的返回值用来决定是否允许显示右键菜单（对于需要对菜单进行权限控制时可能会用到） | Function | |
className | 菜单面板的 className | String | |

### 鼠标配置项

mouse-config | 鼠标配置项 | Object | | 继承 setup.table.mouseConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
selected | 开启单元格选中功能（只对 edit-config.mode=cell 有效） | Boolean | | FALSE

### 按键配置项

keyboard-config | 按键配置项 | Object | | 继承 setup.table.keyboardConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
isArrow | 开启方向键功能 | Boolean | | FALSE
isDel | 开启删除键功能 | Boolean | | FALSE
isEnter | 开启回车键功能 | Boolean | | FALSE
isTab | 开启 Tab 键功能 | Boolean | | FALSE
isEdit | 开启任意键进入编辑（功能键除外） | Boolean | | FALSE
enterToTab | 是否将回车键行为改成 Tab 键行为 | Boolean | | FALSE
editMethod | 只对 isEdit=true 有效，用于重写选中编辑处理逻辑，该函数 Function({row, rowIndex, column, columnIndex, cell})可以返回 false 来阻止默认行为 | Function | |

### 可编辑配置项

edit-config | 可编辑配置项 | Boolean, Object | | 继承 setup.table.editConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
trigger | 触发方式 | String | manual（手动触发方式，只能用于 mode=row）,click（点击触发编辑）,dblclick（双击触发编辑） | click
mode | 编辑模式 | String | cell（单元格编辑模式）,row（行编辑模式） | cell
showIcon | 是否显示列头编辑图标 | Boolean | | TRUE
showStatus | 只对 keep-source 开启有效是否显示单元格值的修改状态 | Boolean | | FALSE
showAsterisk | 是否显示必填字段的红色星号 | boolean | | TRUE
autoClear | 当点击非编辑列之后，是否自动清除单元格的激活状态 | Boolean | | TRUE
activeMethod | 该方法 Function({row, rowIndex, column, columnIndex}) 的返回值用来决定该单元格是否允许编辑 | Function | |
icon | 自定义可编辑列的状态图标 | String | |

### 校验配置项

valid-config | 校验配置项 | Object | |
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
autoPos | 是否自动定位到校验不通过的单元格 | Boolean | | TRUE
message | 校验提示框的方式 | String | default（如果不设置高度，则默认第一行使用 tooltip，之后使用 inline）, none（关闭提示）, inline（强制使用内联的提示）, tooltip（强制使用 tooltip 提示） | default
maxWidth | 校验提示框的最大宽度（对于某些特殊场景可能会用到） | String, Number | | 320

### 校验规则配置项

edit-rules | 校验规则配置项 | {[field: string]: Array\<Object\>} | |
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
required | 是否必填 | Boolean | | FALSE
min | 校验值最小长度（如果 type=number 则比较值大小） | Number | |
max | 校验值最大长度（如果 type=number 则比较值大小） | Number | |
type | 数据校验的类型 | String | number, string, array | string
pattern | 正则校验 | RegExp, String | |
validator | 自定义校验方法 Function({ cellValue, rule, rules, row, rowIndex，column, columnIndex }) 返回一个 Error 或者 Promise\<new Error("提示消息")\> | Promise\<e?: Error\> | |
message | 校验提示内容（支持开启国际化） | String | |
trigger | 触发校验方式（如果为空，则为常规校验方式； 如果指定触发方式，则会在匹配情况下进行校验） | String | blur,change |
maxWidth | 提示框的最大宽度（对于某些特殊场景可能会用到） | Number | | 320

**注意:**

- `trigger`属性在设置为`blur`时, 会在触发相应编辑组件的`blur`事件时进行一次校验.
- 校验时,如果发现校验的结果不满足你的期望,则可以进行下列检查:

1. 单元格的值是否与(你期望的)校验规则匹配? 例如,在编辑`$range-picker`时,如果其校验条件设置为`required: true`
 ,此时,由于`range-picker`在没有选择日期范围时,其值为`[]`,此时验证`required: true`的规则是成功(因为`!![]`为`true`)
 的.那么如果你想要在`[]`的情况下将其验证为失败,则可以通过`validator`进行自定义验证

### 空内容配置项

属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
empty-text | 空数据时显示的内容 | string | |
empty-render | 空内容渲染配置项 | Boolean, Object | | 继承 setup.table.emptyRender
empty-render.name | 渲染器名称 | String | |
empty-render.props | 渲染的参数（请查看目标渲染的 Props） | Object | |
empty-render.attrs | 渲染的属性（请查看目标渲染的 Attribute） | Object | |
empty-render.events | 渲染组件的事件（请查看目标渲染的 Events） | Object | | {}, ...[目标渲染的 arguments]
empty-render.nativeEvents | 渲染组件的原生事件（请查看目标渲染的 Events） | Object | | {}, ...[目标渲染的 arguments]

### 自定义列配置项

custom-config | 自定义列配置项 | Boolean, Object | | 继承 setup.table.customConfig
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
storage | 是否启用 localStorage 本地保存，会将列操作状态保留在本地（需要有 id） | Boolean, Object | |
storage.visible | 启用显示/隐藏列状态 | Boolean | |
storage.resizable | 启用列宽状态 | Boolean | |
checkMethod | 自定义列是否允许列选中的方法，该方法 Function({column}) 的返回值用来决定这一列的 checkbox 是否可以选中 | Function | |

### 横向虚拟滚动配置

scroll-x | 横向虚拟滚动配置 | Object | | 继承 setup.table.scrollX
属性 | 说明 | 类型/返回类型 | 可选值 | 默认值
---|---|---|---|---
gt | 指定大于指定列时自动启动横向虚拟滚动，如果为 0 则总是启用，如果为 -1 则关闭（注：启用横向虚拟滚动之后将不能支持分组表头） | Number | | 60
oSize | 当剩余数据少于指定列时触发重新渲染 | Number | | 默认自动计算
rSize | 每次渲染条数 | Number | | 默认自动计算
vSize | 指定可视区域条数 | Number | | 默认自动计算

### 纵向虚拟滚动配置

scroll-y | 纵向虚拟滚动配置 | Object | | 继承 setup.table.scrollY
属性 | 说明 | 类型/返回类型 | 可选值 | 默认值
---|---|---|---|---
gt | 指定大于指定行时自动启动纵向虚拟滚动，如果为 0 则总是启用，如果为 -1 则关闭（注：启用纵向虚拟滚动之后将不能支持动态行高） | Number | | 100
oSize | 当剩余数据少于指定行时触发重新渲染 | Number | | 默认自动计算
rSize | 每次渲染条数 | Number | | 默认自动计算
vSize | 指定可视区域条数 | Number | | 默认自动计算
adaptive | 自动适配最优的渲染方式 | Boolean | | TRUE

### 插槽 slot

属性 | 说明 | 默认值
---|---|---
empty | 空数据时显示的文本内容 | {}
topBar | 额外的header | {}
bottomBar | 额外的footer | {}

### 事件Events

事件名 | 说明 | 参数
---|---|---
keydown | 当表格被激活且键盘被按下时会触发的事件 | { $event }
current-change | 只对 highlightCurrentRow 有效，当手动选中行并且值发生改变时触发的事件 | { row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event }
radio-change | 只对 type=radio 有效，当手动勾选并且值发生改变时触发的事件 | { row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event }
checkbox-change | 只对 type=checkbox 有效，当手动勾选并且值发生改变时触发的事件 | { records, reserves, indeterminates, checked, row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event }
checkbox-all | 只对 type=checkbox 有效，当手动勾选全选时触发的事件 | { records, reserves, indeterminates, checked, $event }
checkbox-range-start | 只对 checkbox-config.range 有效，当鼠标范围选择开始时会触发的事件 | { records, reserves, $event }
checkbox-range-change | 只对 checkbox-config.range 有效，当鼠标范围选择内的行数发生变化时会触发的事件 | { records, reserves, $event }
checkbox-range-end | 只对 checkbox-config.range 有效，当鼠标范围选择结束时会触发的事件 | { records, reserves, $event }
cell-click | 单元格被点击时会触发该事件 | { row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, triggerRadio, triggerCheckbox, $event }
cell-dblclick | 单元格被双击时会触发该事件 | { row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event }
cell-mouseenter | 当单元格 hover 进入时会触发该事件 | { row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event }
cell-mouseleave | 当单元格 hover 退出时会触发该事件 | { row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event }
header-cell-click | 表头单元格被点击时会触发该事件 | { $rowIndex, column, columnIndex, $columnIndex, triggerResizable, triggerSort, triggerFilter, triggerTreeNode, triggerExpandNode, $event }
header-cell-dblclick | 表头单元格被双击时会触发该事件 | { $rowIndex, column, columnIndex, $columnIndex, $event }
footer-cell-click | 表尾单元格被点击时会触发该事件 | { items, $rowIndex, column, columnIndex, $columnIndex, $event }
footer-cell-dblclick | 表尾单元格被双击时会触发该事件 | { items, $rowIndex, column, columnIndex, $columnIndex, $event }
sort-change | 当排序条件发生变化时会触发该事件 | { column, property, order, $event }
filter-change | 当筛选条件发生变化时会触发该事件 | { column, property, values, datas, filters, $event }
resizable-change | 当列宽拖动发生变化时会触发该事件 | { $rowIndex, column, columnIndex, $columnIndex, $event }
toggle-row-expand | 当行展开或收起时会触发该事件 | { expanded, row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event }
toggle-tree-expand | 当树节点展开或收起时会触发该事件 | { expanded, row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event }
cell-selected | 只对 mouse-config.selected 配置时有效，单元格被选中时会触发该事件 | { row, rowIndex, $rowIndex, column, columnIndex, $columnIndex }
edit-closed | 只对 edit-config 配置时有效，单元格编辑状态下被关闭时会触发该事件 | { row, rowIndex, $rowIndex, column, columnIndex, $columnIndex }
edit-actived | 只对 edit-config 配置时有效，单元格被激活编辑时会触发该事件 | { row, rowIndex, $rowIndex, column, columnIndex, $columnIndex }
edit-disabled | 只对 edit-config 配置时有效，当单元格激活时如果是禁用状态时会触发该事件 | { row, rowIndex, $rowIndex, column, columnIndex, $columnIndex }
valid-error | 只对 edit-rules 配置时有效，当数据校验不通过时会触发该事件 | { rule, row, rowIndex, $rowIndex, column, columnIndex, $columnIndex }
scroll | 表格滚动时会触发该事件 | { type, scrollTop, scrollLeft, isX, isY, $event }
custom | 如果与工具栏关联，在自定义列按钮被手动点击后会触发该事件 | { type, $event}
cell-menu | 只对 menu-config 配置时有效，单元格被鼠标右键时触发该事件 | { type, row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event }
header-cell-menu | 只对 menu-config 配置时有效，表头单元格被鼠标右键时触发该事件 | { type, column, columnIndex, $event }
footer-cell-menu | 只对 menu-config 配置时有效，表尾单元格被鼠标右键时触发该事件 | { type, column, columnIndex, $event }
menu-click | 只对 menu-config 配置时有效，当点击快捷菜单时会触发该事件 { menu, type, row, rowIndex, $rowIndex, column, columnIndex, $columnIndex, $event }

### 方法

方法名称 | 说明 | 返回类型 | 参数
---|---|---|---
loadData(data) | 加载数据（对于表格数据需要重载、局部递增场景下可能会用到） | Promise | data: array
reloadData(data) | 加载数据并清除所有状态（对于表格数据需要重载、局部递增的场景中可能会用到） | Promise | data: array
updateData() | 手动处理数据（对于手动更改了排序、筛选...等条件后需要重新处理数据时可能会用到） | Promise |
syncData() | 同步 data 数据；如果用了该方法，那么组件将不再记录增删改的状态，只能自行实现对应逻辑（对于某些特殊的场景，比如深层树节点元素发生变动时可能会用到） | Promise |
reloadRow(rows, record, field) | 局部加载行数据并恢复到初始状态（对于行数据需要局部更改的场景中可能会用到） | Promise | rows: Row | Row[], record: object, field?: string
reloadExpandContent(rows) | 用于懒加载展开行，重新加载展开行的内容 | Promise | rows: Row | Row[]
reloadTreeChilds(rows) | 用于懒加载树表格，重新加载子节点 | Promise | rows: Row | Row[]
loadColumn(columns) | 加载列配置（对于表格列需要重载、局部递增场景下可能会用到） | Promise | columns: array
reloadColumn(columns) | 加载列配置并恢复到初始状态（对于表格列需要重载、局部递增场景下可能会用到） | Promise | columns: array
refreshColumn() | 刷新列配置（对于动态修改属性、显示/隐藏列等场景下可能会用到） | Promise |
createRow(records) | 创建 Row|Rows 对象（对于某些特殊场景需要对数据进行手动插入时可能会用到） | Promise\<row|rows\> | records: object | array
createData(records) | 创建 data 对象（对于某些特殊场景可能会用到，会自动对数据的字段名进行检测，如果不存在就自动定义） | Promise\<Array\> | records: array
insert(records) | 往表格插入临时数据（不支持深层结构），从第一行插入一行或多行新数据 | Promise\<{row, rows}\> | records?: object | Array\<object\>
insertAt(records, row) | 往表格插入临时数据（不支持深层结构），从指定位置插入一行或多行；第二个参数：row 指定位置（不支持树表格）、null从第一行插入、-1 从最后插入 | Promise\<{row, rows}\> | records: object | Array\<object\>, row?: Row
revertData(rows, field) | 只对 keep-source 开启有效，还原指定行 row 或者整个表格的数据 | Promise | rows: Row | Array\<Row\>, field?: string
remove(rows) | 删除指定行数据（不支持深层结构），指定 row 或 [row, ...] 删除多条数据，如果为空则删除所有数据 | Promise\<{row, rows}\> | rows: Row | Array\<Row\>
removeCheckboxRow() | 删除复选框选中的行数据（不支持深层结构） | Promise\<{row, rows}\> |
removeRadioRow() | 删除单选框选中的行数据（不支持深层结构） | Promise\<{row, rows}\> |
removeCurrentRow() | 删除当前行选中的行数据（不支持深层结构） | Promise\<{row, rows}\> |
removeMergeCells(merges) | 取消单元格的临时合并状态，如果为数组，则取消多个合并 | Promise\<merges\> | merges: {row: Row, col: ColumnInfo} | {row: Row, col: ColumnInfo}[]
removeMergeFooterItems(merges) | 取消表尾的临时合并状态，如果为数组，则取消多个合并 | Promise\<merges\> | merges: {row: Row, col: ColumnInfo} | {row: Row, col: ColumnInfo}[]
getRowIndex(row) | 根据 row 获取相对于 data 中的索引 | Number | row: Row
getVTRowIndex(row) | 根据 row 获取相对于当前数据中的索引 | Number | row: Row
getVMRowIndex(row) | 根据 row 获取相对于当前数据中的索引 | Number | row: Row
getRowNode(tr) | 根据 tr 元素获取对应的 row 信息 | {item, items, index, parent} | tr: Element
getColumns() | 获取表格的可视的列 | Array |
getColid(column) | 根据列获取列的唯一主键 | String | column: ColumnConfig
getColumnById(colid) | 根据列的唯一主键获取列 | Column | colid: string
getColumnByField(field) | 根据列的字段名获取列 | Column | field: string
getTableColumn() | 获取当前表格的列（收集到的全量列、全量表头列、处理条件之后的全量表头列、当前渲染中的表头列） | {collectColumn, fullColumn, visibleColumn, tableColumn} |
getColumnIndex(column) | 根据 column 获取相对于 columns 中的索引 | Number | column: ColumnConfig
getVMColumnIndex(column) | 根据 column 获取渲染中的虚拟索引 | Number | column
getColumnNode(cell) | 根据 th/td 元素获取对应的 column 信息 | {item, items, index, parent} | cell: Element
getSortColumns() | 获取当前排序的所有列信息 | any[] |
getCheckedFilters() | 获取当前筛选的所有列信息 | any[] |
getTableData() | 获取当前表格的数据（完整的全量表体数据、处理条件之后的全量表体数据、当前渲染中的表体数据、当前渲染中的表尾数据） | {fullData, visibleData, tableData, footerData} |
getRowById(rowid) | 根据行的唯一主键获取行 | String | rowid: string
getRowid(row) | 根据行获取行的唯一主键 | Row | row: Row
getData(rowIndex) | 获取数据，和 data 的行为一致，也可以指定索引获取数据 | Array | rowIndex?: number
getRecordset() | 获取表格数据集（获取插入、删除、更改的数据，对于增删改查表格非常方便） | {insertRecords, removeRecords, updateRecords} |
getInsertRecords() | 用于 edit-config，获取插入的临时数据 | Array |
getRemoveRecords() | 获取已删除的数据 | Array |
getUpdateRecords() | 只对 keep-source 开启有效，获取已修改的数据 | Array |
getMergeCells() | 获取临时合并的单元格 | Array\<{row: any, col: ColumnInfo, rowspan: number, colspan: number}\> |
getMergeFooterItems() | 获取临时合并的表尾 | Array\<{row: any, col: ColumnInfo, rowspan: number, colspan: number}\> |
getCurrentColumn() | 用于 highlight-current-column，获取当前列 | ColumnConfig |
getCurrentRecord() | 用于 highlight-current-row，获取高亮的当前行数据 | Row |
getRadioRecord() | 用于 type=radio，获取当已选中的行数据 | Row |
getRadioReserveRecord() | 用于 radio-config.reserve，获取已保留选中的行数据（不包含当前列表） | Row |
getCheckboxRecords() | 用于 type=checkbox，获取已选中的行数据 | Array\<Row\> |
getCheckboxReserveRecords() | 用于 checkbox-config.reserve，获取已保留选中的行数据（不包含当前列表） | Array\<Row\> |
getCheckboxIndeterminateRecords() | 用于 tree-config 和 type=checkbox，获取半选状态的行数据 | Array\<Row\> |
getRowExpandRecords() | 用于 expand-config，用于展开行，获取已展开的行数据 | Array\<Row\> |
getTreeExpandRecords() | 用于 tree-config，用于树表格，获取已展开的节点（注意，即使父节点被收起，只要该节点还处于展开状态都能获取到） | Array\<Row\> |
getActiveRecord() | 用于 edit-config，获取已激活的行数据 | {row,rowIndex,$rowIndex,column,columnIndex,$columnIndex} | row
getSelectedCell() | 用于 mouse-config.selected，获取选中的单元格信息 | {row,column} |
getScroll() | 获取表格的滚动状态 | {virtualX, virtualY, scrollTop, scrollLeft} |
isActiveByRow(row) | 用于 edit-config，判断行是否为激活编辑状态 | Boolean | row
isInsertByRow(row) | 用于 edit-config，判断行是否为插入的临时数据 | Boolean | row: Row
isUpdateByRow(row, field) | 只对 keep-source 开启有效，判断行数据是否发生改变 | Boolean | row: Row, field?: string
isAllCheckboxChecked() | 用于 type=checkbox，判断复选行是否被全部选中 | Boolean |
isCheckedByCheckboxRow(row) | 用于 type=checkbox，判断复选行数据是否勾选 | Boolean | row: Row
isCheckedByRadioRow(row) | 用于 type=radio，判断单选行数据是否勾选 | Boolean | row: Row
isExpandByRow(row) | 用于 expand-config，判断行是否为展开状态 | Boolean | row
isRowExpandLoaded(row) | 用于 expand-config.lazy，用于懒加载展开行，判断展开行是否懒加载完成 | Boolean | row
isTreeExpandByRow(row) | 用于 tree-config，判断行是否为树形节点展开状态 | Boolean | row: Row
isTreeExpandLoaded(row) | 用于 tree-config.lazy，用于懒加载树表格，判断树节点是否懒加载完成 | Boolean | row: Row
isFilter(column) | 判断指定列是否为筛选状态，如果为空则判断所有列 | Boolean | column?: Column
setFilter(column, options) | 用于 filters，修改筛选列表（在筛选条件更新之后可以调用 updateData 函数处理表格数据） | Promise | column: Column, options: []
setActiveRow(row) | 用于 edit-config，激活行编辑，如果是 mode=cell 则默认激活第一个单元格 | Promise | row: Row
setActiveCell(row, field) | 用于 edit-config，激活单元格编辑 | Promise | row: Row, field: string
setSelectCell(row, field) | 用于 mouse-config.selected，选中指定的单元格 | Promise | row: Row, field: string
setMergeCells(merges) | 临时合并单元格，如果为数组则合并多个 | Promise | merges: MergeOptions | MergeOptions[]
setMergeFooterItems(merges) | 临时合并表尾，如果为数组则合并多个 | Promise | merges: MergeOptions | MergeOptions[]
setRowExpand(rows, checked) | 用于 expand-config，设置展开行，二个参数设置这一行展开与否 | Promise | rows: Row | Array\<Row\>, checked: boolean
setAllRowExpand(checked) | 用于 expand-config，设置所有行的展开与否（如果是关闭所有行，可以使用 clearRowExpand 快速清除） | Promise | checked: boolean
setTreeExpand(rows, checked) | 用于 tree-config，设置展开树形节点，二个参数设置这一行展开与否 | Promise | rows: Row | Array\<Row\>, checked: boolean
setAllTreeExpand(checked) | 用于 tree-config，设置所有树节点的展开与否（如果是关闭所有树节点，可以使用 clearTreeExpand 快速清除） | Promise | checked: boolean
setCurrentRow(row) | 用于 highlight-current-row，设置某一行为高亮状态 | Promise | row: Row
setCurrentColumn(column) | 用于 highlight-current-column，设置某列行为高亮状态 | Promise | column: ColumnConfig
setRadioRow(row) | 用于 type=radio，设置某一行为选中状态 | Promise | row: Row
setCheckboxRow(rows, checked) | 用于 type=checkbox，设置行为选中状态，第二个参数为选中与否 | Promise | rows: Row | Array\<Row\>, checked: boolean
setAllCheckboxRow(checked) | 用于 type=checkbox，设置所有行的选中状态 | Promise | checked: boolean
toggleCheckboxRow(row) | 用于 type=checkbox，切换某一行的选中状态 | Promise | row: Row
toggleAllCheckboxRow() | 用于 type=checkbox，切换所有行的选中状态 | Promise |
toggleRowExpand(row) | 用于 type=expand，切换展开行的状态 | Promise | row: Row
toggleTreeExpand(row) | 用于 tree-config，切换展开树形节点的状态 | Promise | row: Row
clearMergeCells() | 手动清除临时合并的单元格 | Promise |
clearMergeFooterItems() | 手动清除临时合并的表尾 | Promise |
clearCurrentRow() | 用于 highlight-current-row，手动清空当前高亮的状态 | Promise |
clearCurrentColumn() | 用于 highlight-current-column，手动清空当前高亮的状态 | Promise |
clearRadioRow() | 用于 type=radio，手动清空用户的选择 | Promise |
clearRadioReserve() | 用于 radio-config.reserve，手动清空用户保留选中的行数据 | Promise |
clearCheckboxRow() | 用于 type=checkbox，手动清空用户的选择 | Promise |
clearCheckboxReserve() | 用于 checkbox-config.reserve，手动清空用户保留选中的行数据 | Promise |
clearRowExpand() | 用于 type=expand，手动清空展开行状态，数据会恢复成未展开的状态 | Promise |
clearRowExpandLoaded(row) | 用于 expand-config.lazy，手动清空懒加载展开行的状态，数据会恢复成未展开的状态，当再次展开时会重新加载 | Promise | row: any
clearTreeExpand() | 用于 tree-config，手动清空树形节点的展开状态，数据会恢复成未展开的状态 | Promise |
clearTreeExpandLoaded(row) | 用于 tree-config.lazy，手动清空懒加载树节点的状态，数据会恢复成未展开的状态，当再次展开时会重新加载 | Promise | row: any
clearSort() | 手动清空排序条件，数据会恢复成未排序的状态 | Promise |
clearFilter(column) | 手动清空筛选条件（如果不传 column 则清空所有筛选条件），数据会恢复成未筛选的状态 | Promise | column?: ColumnConfig
clearSelected() | 手动清除单元格选中状态 | Promise |
clearActived() | 手动清除单元格激活状态 | Promise |
clearData(rows, field) | 手动清空单元格内容，如果不创参数，则清空整个表格内容，如果传了行则清空指定行内容，如果传了指定字段，则清空该字段内容 | Promise | rows?: Row | Array\<Row\>, field?: string
clearScroll() | 手动清除滚动相关信息，还原到初始状态 | Promise |
clearValidate() | 手动清除校验 | Promise |
clearAll() | 手动清除表格所有条件，还原到初始状态（对于增删改查的场景中可能会用到，比如在数据保存之后清除表格缓存） | Promise |
closeFilter() | 手动关闭筛选面板（某些特殊场景可能会用到） | Promise |
clostTooltip() | 手动关闭 tooltip 提示（某些特殊场景可能会用到） | Promise |
closeMenu() | 手动关闭快捷菜单（某些特殊场景可能会用到） | Promise |
updateFooter() | 手动更新表尾（对于某些需要频繁更新的场景下可能会用到） | Promise |
updateStatus(scope) | 更新单元格状态（当使用自定义渲染时可能会用到） | Promise | scope: { row, column }
hideColumn(column) | 隐藏指定列 | Promise | column: ColumnConfig
showColumn(column) | 显示指定列 | Promise | column: ColumnConfig
scrollTo(scrollLeft, scrollTop) | 如果有滚动条，则滚动到对应的位置 | Promise | scrollLeft?: number, scrollTop?: number
scrollToRow(row, column) | 如果有滚动条，则滚动到对应的行（对于某些特定的场景可能会用到，比如定位到某一行） | Promise | row: Row, column?: ColumnConfig
scrollToColumn(column) | 如果有滚动条，则滚动到对应的列（对于某些特定的场景可能会用到，比如定位到某一列） | Promise | column: ColumnConfig
sort(field, order) | 手动对表格进行排序（如果 order 为空则自动切换排序） | Promise | field: string, order?: 'desc' | 'asc'
isSort(column) | 判断指定列是否为排序状态，如果为空则判断所有列 | Boolean | column?: string | ColumnInfo
recalculate(refull) | 重新计算表格，如果传 true 则进行完整计算（对于某些特殊场景可能会用到，比如隐藏的表格、重新计算列宽...等） | Promise | refull?: boolean
refreshScroll() | 刷新滚动操作，手动同步滚动相关位置（对于某些特殊的操作，比如滚动条错位、固定列不同步） | Promise |
validate(rows, callback) | 快速校验，如果存在记录不通过的记录，则返回不再继续校验（异步校验除外）；如果第一个参数为 true 则校验当前表格数据，如果指定 row 或 rows 则校验指定行或多行，如果不指定数据，则默认只校验临时变动的数据，例如新增或修改，例如新增或修改。该回调函数会在校验结束后被调用 callback(errMap)。若不传入回调函数，则会返回一个 promise | Promise\<ErrMap\> | rows?: Row | Row[], callback?: Function
fullValidate(rows, callback) | 完整校验，和 validate 的区别就是默认校验当前表格数据并且给有效数据中的每一行进行校验 | Promise\<ErrMap\> | rows?: Row | Row[], callback?: Function
connect(toolbar) | 连接工具栏 | Promise | toolbar: Toolbar
focus() | 使表格获取焦点 | Promise |
blur() | 使表格失去焦点 | Promise |
 [resetColumn(options)](#resetColumn) | 手动重置列的显示隐藏、列宽拖动的状态；如果为 true 则重置所有状态（如果已关联工具栏，则会同步更新） | Promise | options: boolean \| object
[exportData(options)](#exportData) | 将表格数据导出（只支持基本数据结构，目前不支持分组、合并等；树结构和虚拟滚动只允许导出数据源）,如果需要导出xls/xlsx,则需要按照`excel-util`的[generateExcelByTable](process.env.VUE_APP_PUBLIC_PATH/components/excel-util-cn/#generateExcelByTable) | Promise | | options: object
getExportColumns() | 获取导出列的定义(仅用于[generateExcelByTable](process.env.VUE_APP_PUBLIC_PATH/components/excel-util-cn/#generateExcelByTable)方法) | void | -
[openExport(options)](#openExport) | 打开高级导出（只对 export-config 启用后有效） | Promise | | options: object
[importData(options)](#importData) | 将数据导入表格（只支持基本数据结构，目前不支持分组、合并等） | Promise | | options: object
[print(options)](#print) | 打印（只支持基本数据结构，目前不支持分组、合并等） | Promise | | options: object
[saveFile(options)](#saveFile) | 保存文件到本地 | Promise\<any\> | | options: object
[readFile(options)](#readFile) | 读取本地文件 | Promise\<{ file, files }\> | | options: object

**注意:**

-
在使用exportData时,对于big-table来说,可以传入一个额外的el参数,用于确定需要导出的table的DOM节点,其他使用方法与`excel-util`
的`generateExcelByTable`完全一致,例如:

```javascript
const {
 col,
 columns,
} = this.$refs.xTable.getExportColumns()
this.$refs.xTable.exportData({
 el: this.$refs.xTable.$el.querySelector(= '.vxe-table--main-wrapper .vxe-table--body-wrapper table'), // 仅适用于big-table的exportData方法
 fileType: '.xlsx', // 设置文件类型
 fileName: '文件名', // 设置导出的文件名
 header: {
 col,
 // col: ['checkbox', 'seq', 'name', 'sex', 'loginId', 'namePath'], // 列说明，若未传入列说明，且表格数据为空将会报错
 columns,
 // columns: [{seq: 'title', name: 'Name', sex: 'Sex', loginId: '账号', namePath: '组织路径', }], // 如果seq列配置了title,则使用title属性的值定义,否则一定要写一个'#'
 exclude: ['name',], // 排除列
 },
})
```

- 你可以使用`getExportColumns`方法来获取上述的`col`及`columns`配置, 当然你也可以自行构建`col`和`columns`
 数组,但是需要注意的是,如果表格包含`seq`列,那么`seq`列必须在`columns`中有值(`#`或配置的`title`属性的值)
 ,否则会导致这个导出的`excel`文件不能再被导入

### resetColumn ###

options 参数
参数 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
visible | 是否重置可视列状态 | Boolean | | TRUE
resizable | 是否重置列宽拖动状态 | Boolean | | FALSE

### exportData ###

options 参数
参数 | 说明 | 类型 | 可选值 | 默认值 | 版本 |
---|---|---|---|---|---|
filename | 文件名 | String | | | - |
sheetName | 表名（只对支持的文档类型有效） | String | | | - |
type | 文件类型 | String | csv, html, xml, txt | csv | - |
types | 可选文件类型列表 | Array | csv, html, xml, txt | ['csv', 'html', 'xml', 'txt'] | - |
mode | 输出数据的方式 | String | current, selected, all | current | - |
modes | 输出数据的方式列表 | Array | current, selected, all | ['current', 'selected', 'all'] | - |
original | 是否为源数据（某些场景下支持 true， 比如虚拟滚动、优化的固定列..，如果需要支持导入，则必须设置为 true） | Boolean | | FALSE | - |
message | 是否显示内置的消息提示 | Boolean | | FALSE | - |
isHeader | 是否需要表头 | Boolean | | TRUE | - |
isFooter | 是否需要表尾 | Boolean | | TRUE | - |
download | 是否马上下载，如果设置为 false 则通过返回结果为内容的 Promise | Boolean | | TRUE | - |
data | 自定义数据 | Array | | | - |
columns | 自定义列（如果指定了 columns 则 columnFilterMethod 默认为空） | Array | | | - |
columnFilterMethod | 列过滤方法，该函数 Function({ column, $columnIndex }) 的返回值用来决定是否过滤掉列 | Function | | 默认过滤掉 type=seq,checkbox,radio 和 field 为空的列 | - |
dataFilterMethod | 数据过滤方法，该函数 Function({ row, $rowIndex }) 的返回值用来决定是否过滤掉数据行 | Function | | | - |
footerFilterMethod | 表尾过滤方法，该函数 Function({ items, $rowIndex }) 的返回值用来决定是否过滤掉表尾行 | Function | | | - |
remote | 是否服务端导出 | Boolean | | FALSE | - |
exportMethod | 只对 remote=true 有效，该函数 Function({ options }) 用于自定义导出或服务端导出，返回 Promise | Function | | | - |
style | 只对 type=html 有效，自定义文档的 css 样式信息 | string | | | - |
raw | 对于excel导出,是否将其中的超长数字数据(例如身份证等)转换为科学计数法表示,true表示导出的不是科学计数法显示.(例如,表格中的一个数据: `12345678901234567890`, 在`raw`为`true`时,会导出为`12345678901234567890`;为`false`时,会被导出为`1.23457E+19`). | Boolean | | TRUE | 在`1.5.151`及之前的版本中,由于不存在此参数,即其默认值相当于`false`,在`1.5.152`版本开始,添加了此参数且其默认值设置为`true` |

### openExport ###

options 参数
参数 | 说明 | 类型 | 可选值 | 默认值 | 版本 |
---|---|---|---|---|---|
filename | 文件名 | String | | - |
sheetName | 表名（只对支持的文档类型有效） | String | | - |
type | 文件类型 | String | csv, html, xml, txt | csv | - |
types | 可选文件类型列表 | Array | csv, html, xml, txt | ['csv', 'html', 'xml', 'txt'] | - |
mode | 输出数据的方式 | String | current, selected, all | current | - |
modes | 输出数据的方式列表 | Array | current, selected, all | ['current', 'selected', 'all'] | - |
original | 是否为源数据（某些场景下支持 true， 比如虚拟滚动、优化的固定列..，如果需要支持导入，则必须设置为 true） | Boolean | | FALSE | - |
message | 是否显示内置的消息提示 | Boolean | | FALSE | - |
isHeader | 是否需要表头 | Boolean | | TRUE | - |
isFooter | 是否需要表尾 | Boolean | | TRUE | - |
remote | 是否服务端导出 | Boolean | | FALSE | - |
exportMethod | 只对 remote=true 有效，该函数 Function({ options }) 用于自定义导出或服务端导出，返回 Promise | Function | | | - |
style | 只对 type=html 有效，自定义文档的 css 样式信息 | string | | | - |
isPrint | 是否需要打印按钮 | Boolean | | TRUE | - |
raw | 对于excel导出,是否将其中的超长数字数据(例如身份证等)转换为科学计数法表示,true表示导出的不是科学计数法显示.(例如,表格中的一个数据: `12345678901234567890`, 在`raw`为`true`时,会导出为`12345678901234567890`;为`false`时,会被导出为`1.23457E+19`). | Boolean | | TRUE | 在`1.5.151`及之前的版本中,由于不存在此参数,即其默认值相当于`false`,在`1.5.152`版本开始,添加了此参数且其默认值设置为`true` |

**注意:**

1. 导出`excel`时,`export-config`的所有属性都将会传递给导出方法

### importData ###

options 参数
参数 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
mode | 导入数据的方式 | String | covering, insert | covering
message | 是否显示内置的消息提示 | Boolean | | FALSE
types | 导入的文件类型列表 | Array | csv, html, xml, txt | ['csv', 'html', 'xml', 'txt']
remote | 是否服务端导入 | Boolean | | FALSE
importMethod | 只对 remote=true 有效，该函数 Function({ file, options }) 用于自定义导入或服务端导入，返回 Promise | Function | |
openImport(options) | 打开高级导入（只对 import-config 启用后有效） | Promise | | options: object
mode | 导入数据的方式 | String | covering, insert | covering
message | 是否显示内置的消息提示 | Boolean | | FALSE
types | 导入的文件类型列表 | Array | csv, html, xml, txt | ['csv', 'html', 'xml', 'txt']
remote | 是否服务端导入 | Boolean | | FALSE
importMethod | 只对 remote=true 有效，该函数 Function({ file, options }) 用于自定义导入或服务端导入，返回 Promise | Function | |

### print ###

options 参数
参数 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
sheetName | 表名（只对支持的文档类型有效） | String | |
mode | 输出数据的方式 | String | current, selected, all | current
modes | 输出数据的方式列表 | Array | current, selected, all | ['current', 'selected', 'all']
original | 是否为源数据（某些场景下支持 true， 比如虚拟滚动、优化的固定列..，如果需要支持导入，则必须设置为 true） |
Boolean | | FALSE
isHeader | 是否需要表头 | Boolean | | TRUE
isFooter | 是否需要表尾 | Boolean | | TRUE
data | 自定义数据 | Array | |
columns | 自定义列（如果指定了 columns 则 columnFilterMethod 默认为空） | Array | |
columnFilterMethod | 列过滤方法，该函数 Function({ column, $columnIndex }) 的返回值用来决定是否过滤掉列 | Function | | 默认过滤掉 type=seq,checkbox,radio 和 field 为空的列
dataFilterMethod | 数据过滤方法，该函数 Function({ row, $rowIndex }) 的返回值用来决定是否过滤掉数据行 | Function | |
footerFilterMethod | 表尾过滤方法，该函数 Function({ items, $rowIndex }) 的返回值用来决定是否过滤掉表尾行 | Function | |
style | 只对 type=html 有效，自定义文档的 css 样式信息 | string | |
content | 自定义打印的内容 | string | |
beforePrintMethod | 该函数 Function({ content, options }) 会在打印之前触发，可以通过返回自定义打印的内容 | ({ content, options }) =\> string | |

### saveFile ###

options 参数
参数 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
filename | 文件名 | string | |
type | 文件类型 | string | |
content | 内容 | string | Blob | |

### readFile ###

options 参数
参数 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
multiple | 是否允许多选 | Boolean | | FALSE
types | 支持选取的文件类型 | Array | | ['csv', 'html', 'xml', 'txt']
message | 是否显示内置的消息提示 | Boolean | | TRUE


### 工具条

big-table-toolbar 工具条属性
属性 | 说明 | 类型 | 可选值 | 默认值
---|---|---|---|---
import | 导入按钮配置（需要设置 "import-config"） | Boolean, Object | | 默认继承 setup.toolbar.import
import.icon | 自定义图标 | String | |
export | 导出按钮配置（需要设置 "export-config"） | Boolean, Object | | 默认继承 setup.toolbar.export
export.icon | 自定义图标 | String | |
print | 打印按钮配置 | Boolean, Object | | 默认继承 setup.toolbar.print
print.icon | 自定义图标 | String | |
custom | 自定义列配置 | Boolean, Object | | 默认继承 setup.toolbar.custom
custom.trigger | 触发方式 | String | manual,click,hover | click
custom.immediate | 列勾选之后是否实时同步 | Boolean | | FALSE
custom.isFooter | 是否显示底部操作按钮 | Boolean | | TRUE
custom.icon | 自定义图标 | String | |
buttons | 左侧按钮按钮列表插槽 | | | {}
tools | 右侧工具列表插槽 | | | {}
fullscreen| 是否展示全屏按钮| Boolean, Object | |
fullscreen.icon| 自定义全屏图标 | string | |
fullscreen.iconExit| 自定义全屏退出图标 | string | |
