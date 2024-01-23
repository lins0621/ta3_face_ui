<script lang='jsx'>
  import Basic from './basic.md';
  import Size from './size.md';
  import Seq from './seq.md';
  import Width from './width.md';
  import Tooltip from './tooltip.md';
  import Ellipsis from './ellipsis.md';
  import Border from './border.md';
  import CellStyle from './cell-style.md';
  import Resizable from './resizable.md';
  import AutoHeight from './auto-height.md';
  import FixColumn from './fix-column.md';
  import Group from './group.md';
  import Radio from './radio.md';
  import Checkbox from './checkbox.md'
  import Sort from './sort.md'
  import Filter from './filter.md'
  import ColumnFilter from './filter-column.md'
  import Format from './format.md'
  import CollectionType from './collectionType.md'
  import SimpleEdit from './simpletEdit.md'
  import TreeEditTable from './treeEditTable.md'
  import EditWithConfig from './editWithConfig.md'
  import TableOperateEdit from "./tableOperateEdit.md"
  import EditWithConfigEvent from './editWithConfigEvent.md'
  import EditCustomTemplate from './editCustomTemplate.md'
  import CustomControlOperateTable from './customControlOperateTable.md'
  import getPopupContainerInEdit from './getPopupContainerInEdit.md'
  import EditWithSlot from './editWithSlot.md'
  import OperateTable from './operate-table.md'
  import KeyboardOperate from './keyboardOperate.md'
  import FooterSummary from './footerSummary.md'
  import Pagination from './pagination.md'
  import PaginationExtra from './paginationExtra.md'
  import Event from './event.md'
  import SelfTemplate from './self-template.md'
  import MergeRowsOrColumns from './mergeRowsOrColumns.md'
  import RightClickMenu from './rightClickMenu.md'
  import TreeLine from './treeLine.md'


  import TreeExpand from './treeExpand.md'
  import TreeSelect from './treeSelect.md'
  import TreeFilter from './treeFilter.md'
  import TreeSort from './treeSort.md'
  import TreeGroupSummary from './treeGroupSummary.md'
  import TreeAsyncLoad from './treeAsyncLoad.md'

  import ExpandRow from './expand-row.md'
  import ExpandTable from './expand-table.md'
  import Tool from './tool.md'
  import ImportAndExport from './import-export.md'
  import Print from './print.md'

  import VirtualBase from './virtualBase.md'
  import VirtualRenderDemo from './virtualRenderDemo.md'
  import Virtual from './virtual.md'
  import RenderColumnWidth from './renderColumnWidth.md'
  import ExportAllData from './export-all-data.md'
  import ShowHideColunm from './show-hide-colunm.md'
  import TableColumnBtArray from './table-column-by-array.md'
  import ColumnArrayCustomrender from './column-array-customrender.md'
  import columnControl from './columnsControl.md'
  import columnsControlSave from './columnsControlSave.md'
  import EditLinkage from './editLinkage.md'

  import Type from './type.md'
  import CustomType from './custom-type.md'
  import HideColumnsInExpand from './hideColumnsInExpand.md'
  import LineDraggable from './draggable.md'




  import CN from './../index.zh-CN.md';
  import US from './../index.en-US.md';


  const md = {
    cn: `# BigTable 大数据表格
         - 组件vue标签为：\`<ta-big-table></ta-big-table>\`
         - ta-big-table,支持大数据显示的表格
         ## 何时使用
         - 页面需要表格显示数据时
         - 支持大数据量显示
         - 支持数据编辑,导出,导入,打印
         - 支持合计,排序,自定义模板等功能

## 按需引入组件
          在使用\`@yh/babel-plugin-ui-import\`或\`@yh/vite-plugin-ui-importer\`插件时,可通过如下代码进行自动引入
          \`\`\`JavaScript
          import { BigTable, } from '@yh/ta404-ui';
          \`\`\`
          也可以通过如下代码进行引入
          \`\`\`JavaScript
          import BigTable from '@yh/ta404-ui/es/big-table';
          import '@yh/ta404-ui/es/big-table/style';
          Vue.use(BigTable);
          \`\`\`
         ## 代码演示
        `,
    us: `# BigTable
         Small numerical value or status descriptor for UI elements.
         ## When To Use
         Badge normally appears in proximity to notifications or user avatars with eye-catching appeal, typically displaying unread messages count.
         ## Examples
        `,
  };

  export default {
    category: 'Components',
    subtitle: '大数据表格',
    type: 'Data Display',
    zhType: '数据展示',
    title: 'BigTable',
    render () {
      return (
        <div >
          <mD cn={md.cn} us={md.us} />
          <Basic />
          <Size />
          <Seq />
          <Type />
          <CustomType />
          <Width />
          <Ellipsis />
          <Tooltip />
          <Border />
          <CellStyle />
          <Resizable />
          <AutoHeight />
          <FixColumn />
          <Group />
          <Radio />
          <Checkbox />
          <Sort />
          <ColumnFilter/>
          <Filter/>
          <Format/>
          <CollectionType/>
          <EditWithConfig/>
          <EditWithConfigEvent/>
          <EditLinkage/>
          <EditCustomTemplate/>
          <TableOperateEdit/>
          <CustomControlOperateTable/>
          <SimpleEdit/>
          <TreeEditTable/>
          <getPopupContainerInEdit/>
          <OperateTable/>
          <TableColumnBtArray />
          <ColumnArrayCustomrender />
          <KeyboardOperate/>
          <EditWithSlot/>
          <FooterSummary/>
          <Pagination/>
          <PaginationExtra/>
          <Event/>
          <SelfTemplate/>
          <MergeRowsOrColumns/>
          <ShowHideColunm/>
          <RightClickMenu/>
          <TreeLine/>
          <TreeExpand/>
          <TreeSelect/>
          <TreeFilter/>
          <TreeSort/>
          <TreeGroupSummary/>
          <TreeAsyncLoad/>
          <ExpandRow/>
          <ExpandTable/>
          <Tool/>
          <ExportAllData/>
          <ImportAndExport/>
          <Print/>
          <VirtualBase/>
          <VirtualRenderDemo/>
          <Virtual/>
          <RenderColumnWidth/>
          <LineDraggable/>
          <columnControl />
          <columnsControlSave />
          <HideColumnsInExpand />
        <api>
          <CN slot='cn' />
          <US />
        </api>
      </div>
    );
    },
  };
</script>
