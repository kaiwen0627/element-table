<template>
  <el-table
    :data="tableData"
    style="width: 100%"
    class="common-table-main"
    v-bind="$attrs"
    v-on="$listeners"
    @sort-change="sortChange"
    @selection-change="selectionChange"
  >
    <!-- 复选框 -->
    <el-table-column
      type="selection"
      style="width: 55px;"
      v-if="tableConfig.config.showCheckBox"
    />
    <!-- 索引 -->
    <el-table-column
      width="60"
      align="center"
      type="index"
      v-if="tableConfig.config.showIndex"
      :label="`序号`"
    />
    <el-table-column
      v-for="column in columns"
      :show-overflow-tooltip="true"
      :prop="column.prop"
      :label="column.name"
      :key="column.prop"
      :width="column.width"
      :sortable="column.sortable || false"
      :resizable="column.resizable || false"
    >
      <!-- 自定义当前列表头 -->
      <template slot="header" slot-scope="scope">
        <slot
          v-if="column.headSlotName"
          :name="column.headSlotName"
          :rowData="scope"
        ></slot>
        <!-- 展示表格数据文本 -->
        <span v-else class="show-text">{{ column.name }}</span>
      </template>
      <!-- 有插槽时，展示插槽内容 -->
      <template slot-scope="scope">
        <slot
          v-if="column.slotname"
          :name="column.slotname"
          :rowData="scope"
        ></slot>
        <!-- 展示表格数据文本 -->
        <span v-else class="show-text">{{ scope.row[column.prop] }}</span>
      </template>
    </el-table-column>
  </el-table>
</template>
<script>
export default {
  props: {
    tableConfig: {
      require: true,
      type: Object,
    },
  },
  mounted() {},
  components: {},
  data() {
    return {
      tableData: [], //表格数据
      columns: {},
    };
  },
  watch: {
    tableConfig: {
      immediate: true,
      deep: true,
      handler: function(newVal, oldVal) {
        this.dealTableConfig(newVal, oldVal);
      },
    },
  },
  methods: {
    dealTableConfig(newVal) {
      console.log("newVal.config.columns", newVal.config.columns);
      this.tableData = newVal.data;
      this.columns = (newVal.config.columns || []).filter((ele) => !ele.hide);
    },
    // 排序改变事件
    sortChange({ column, prop, order }) {
      let data = { column, prop, order };
      this.$emit("sortChange", data);
    },
    // 选择项变化
    selectionChange(selection) {
      console.log("selection", selection);
    },
  },
};
</script>
<style lang="scss"></style>
