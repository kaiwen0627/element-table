<template>
  <div id="app">
    <!-- 组件可直接绑定 Table Attributes-->
    <common-table :tableConfig="tableConfig" :stripe="true" :border="true">
      <template #editSlot="rowData">
        <div>
          <button @click="binaji(rowData)">编辑</button>
        </div>
      </template>
    </common-table>
  </div>
</template>

<script>
import CommonTable from "./components/Table.vue";

export default {
  name: "App",
  components: {
    CommonTable,
  },
  data() {
    return {
      tableConfig: {
        config: {
          showIndex: true, //是否显示行号
          showCheckBox: true, //是否显示多选框
          columns: [
            {
              name: "日期",
              prop: "date",
              width: 300,
              sortable: true,
              resizable: true,
            },
            {
              name: "姓名",
              prop: "name",
              width: 150,
              hide: true, //是否隐藏列
            },
            {
              name: "地址",
              prop: "address",
            },
            {
              slotname: "editSlot", // 自定义插槽列
              name: "操作",
            },
          ],
        },
        data: [
          {
            date: "2016-05-02",
            name: "王小虎",
            address: "上海市普陀区金沙江路 1518 弄",
          },
          {
            date: "2016-05-04",
            name: "王小虎",
            address: "上海市普陀区金沙江路 1517 弄",
          },
          {
            date: "2016-05-01",
            name: "王小虎",
            address: "上海市普陀区金沙江路 1519 弄",
          },
          {
            date: "2016-05-03",
            name: "王小虎",
            address: "上海市普陀区金沙江路 1516 弄",
          },
        ],
      },
    };
  },
  methods: {
    binaji(data) {
      console.log("data", data);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
