<template>
  <div>
    <div>
      <span>桌台查询：</span>
      <el-input v-model="searchKey" size="mini" placeholder="请输入桌台名称查询" style="width: 200px" class="input-with-select">
        <el-button slot="append" icon="el-icon-search" />
      </el-input>
      <span style="margin-left: 20px;">门店名称：</span>
      <el-select v-model="shop" size="mini" style="width: 200px" placeholder="请选择所属门店">
        <el-option
          v-for="item in shops"
          :key="item.value"
          :label="item.name"
          :value="item.id"
        />
      </el-select>
    </div>
    <div style="margin: 10px 0">
      <el-button size="mini" type="primary" icon="el-icon-plus" @click="toAddTable">添加桌台</el-button>
      <el-select
        v-model="set"
        size="mini"
        multiple
        collapse-tags
        style="margin-left: 20px;"
        placeholder="批量操作"
      >
        <el-option
          v-for="item in setArr"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        />
      </el-select>
    </div>
    <div>
      <el-table
        ref="multipleTable"
        :header-row-style="{
          'background-color': '#FAFAFA'
        }"
        size="mini"
        :data="tableData"
        tooltip-effect="dark"
        style="width: 100%"
        @selection-change="handleSelectionChange"
      >
        <el-table-column
          type="selection"
          width="55"
        />
        <el-table-column
          prop="name"
          label="门店名称"
          min-width="120"
        />
        <el-table-column
          prop="name"
          label="桌台"
          min-width="120"
        />
        <el-table-column
          label="设备状态"
          min-width="120"
        >
          <template slot-scope="scope">
            <el-switch
              v-model="scope.row.id"
              disabled
            />
          </template>
        </el-table-column>
        <el-table-column
          fixed="right"
          label="操作"
          width="150"
          align="center"
        >
          <template slot-scope="scope">
            <el-button type="text" size="small" @click.native.prevent="editRow(scope.row)">编辑</el-button>
            <el-button type="text" size="small" @click.native.prevent="seeQRcodeRow(scope.row)">二维码</el-button>
            <el-button type="text" size="small" @click.native.prevent="deleteRow(scope.row)">删除</el-button>
          </template>
        </el-table-column>
      </el-table>
      <div class="page">
        <el-pagination
          :current-page="currentPage"
          :page-sizes="[10, 20, 50, 100]"
          :page-size="pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="totalCells"
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
        />
      </div>
      <!--        <div style="margin-top: 20px">-->
      <!--          <el-button @click="toggleSelection([tableData[1], tableData[2]])">切换第二、第三行的选中状态</el-button>-->
      <!--          <el-button @click="toggleSelection()">取消选择</el-button>-->
      <!--        </div>-->
    </div>
   <!-- add edit-->
    <el-dialog
      :title="addEditTitle"
      :visible.sync="addEditTableShow"
      v-if="addEditTableShow"
      width="450px">
      <div>
        <add-edit-table :addEdit="addEdit" v-model="addEditTableShow" @getFatherData="getTableData" />
      </div>
    </el-dialog>
    <!--二维码-->
    <el-dialog
      title="桌台二维码"
      :visible.sync="qrCodeShow"
      width="300px">
      <div style="height: 150px" />
      <div style="text-align: right">
        <el-button size="mini">下载二维码</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import AddEditTable from './components/addEditTable'
export default {
  name: 'TableList',
  components: { AddEditTable },
  data() {
    return {
      searchKey: '',
      shop: '',
      shops: [
        { id: 1, name: '门店1' },
        { id: 2, name: '门店2' },
        { id: 3, name: '门店3' },
        { id: 4, name: '门店4' }
      ],
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
      totalCells: 110,
      addEditTitle: '',
      addEditTableShow: false,
      addEdit: {},
      qrCodeShow: false
    }
  },
  created() {
  },
  mounted() {
  },
  methods: {
    getTableData() {
      console.log(12344)
    },
    toAddTable() {
      this.addEdit = {}
      this.addEditTitle = '添加桌台'
      this.addEditTableShow = true
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
    editRow(item) {
      this.addEdit = item
      this.addEditTitle = '编辑桌台'
      this.addEditTableShow = true
    },
    seeQRcodeRow(item) {
      this.qrCodeShow = true
    },
    deleteRow(row) {
      this.$confirm('此操作将永久删除该桌台【' + row.name + '】, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.$message({
          type: 'success',
          message: '删除成功!'
        });
      }).catch(() => {});
    },
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`)
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`)
    }
  }
}
</script>

<style scoped>

</style>
