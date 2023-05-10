<template>
  <div>
    <div>
      <span>门店名称：</span>
      <el-input size="mini" placeholder="请输入门店名称查询" style="width: 275px" v-model="searchKey" class="input-with-select">
        <el-button slot="append" icon="el-icon-search"></el-button>
      </el-input>
    </div>
    <div style="margin-top: 15px">
      <el-table
        :header-row-style="{
          'background-color': '#FAFAFA'
        }"
        size="mini"
        ref="multipleTable"
        :data="tableData"
        tooltip-effect="dark"
        style="width: 100%"
        @selection-change="handleSelectionChange">
        <el-table-column
          type="selection"
          width="55">
        </el-table-column>
        <el-table-column
          prop="name"
          label="门店名称"
          min-width="120">
        </el-table-column>
        <el-table-column
          prop="name"
          label="桌台"
          min-width="120">
        </el-table-column>
        <el-table-column
          prop=""
          label="设备状态"
          min-width="120">
        </el-table-column>
        <el-table-column
          fixed="right"
          label="操作"
          width="150"
          align="center">
          <template slot-scope="scope">
            <el-button
              @click.native.prevent="stateRow(scope.row)"
              type="text"
              size="small">
              启用
            </el-button>
            <el-button
              @click.native.prevent="editRow(scope.row)"
              type="text"
              size="small">
              编辑
            </el-button>
          </template>
        </el-table-column>
      </el-table>
      <div class="page">
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage"
          :page-sizes="[10, 20, 50, 100]"
          :page-size="pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="totalCells">
        </el-pagination>
      </div>
      <!--        <div style="margin-top: 20px">-->
      <!--          <el-button @click="toggleSelection([tableData[1], tableData[2]])">切换第二、第三行的选中状态</el-button>-->
      <!--          <el-button @click="toggleSelection()">取消选择</el-button>-->
      <!--        </div>-->
    </div>
  </div>
</template>

<script>
export default {
  name: 'BaseSet',
  data() {
    return {
      searchKey: '',
      set: '',
      setArr: [
        {
          value: '选项1',
          label: '选项1'
        }, {
          value: '选项2',
          label: '选项2'
        }, {
          value: '选项3',
          label: '选项3'
        }
      ],
      tableData: [
        {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-08',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-06',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-07',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }
      ],
      multipleSelection: [],
      pageSize: 10,
      currentPage: 1,
      totalCells: 110
    }
  },
  created() {
  },
  mounted() {
  },
  methods: {
    toAddTable(){
      this.$router.push({path: '/shop/addPrinter'})
    },
    toggleSelection(rows) {
      if (rows) {
        rows.forEach(row => {
          this.$refs.multipleTable.toggleRowSelection(row)
        })
      } else {
        this.$refs.multipleTable.clearSelection()
      }
    },
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    editRow (item) {},
    stateRow(item) {},
    deleteRow(row) {},
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
    }
  }
}
</script>

<style scoped>

</style>
