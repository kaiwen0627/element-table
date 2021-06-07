<template>
  <el-table
    :data="tableData"
    style="width: 100%"
    class="common-table-main"
    v-bind="$attrs"
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
      <template v-if="column.slotname" slot-scope="scope">
        <slot :name="column.slotname" :rowData="scope"></slot>
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
    selectionChange(selection) {
      console.log("selection", selection);
    },
  },
};
</script>
<style lang="scss"></style>
