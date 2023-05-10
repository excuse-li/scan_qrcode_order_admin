<template>
  <div>
    <div>
      <el-button size="mini" type="primary" icon="el-icon-plus" @click="addDishes">添加菜谱</el-button>
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
          label="菜谱名称"
          min-width="120"
        />
        <el-table-column
          prop="state"
          label="使用状态"
          sortable
          min-width="120"
        />
        <el-table-column
          prop=""
          label="菜品数量"
          min-width="120"
        />
        <el-table-column
          prop=""
          label="菜谱授权门店"
          min-width="120"
        />
        <el-table-column
          prop=""
          label="最近变更时间"
          min-width="140"
        />
        <el-table-column
          fixed="right"
          label="操作"
          width="250"
          align="center"
        >
          <template slot-scope="scope">
            <el-button type="text" size="small">设置菜品</el-button>
            <el-button type="text" size="small" @click="limitRow(scope.row)">授权管理</el-button>
            <el-button type="text" size="small">复制</el-button>
            <el-button type="text" size="small">启用</el-button>
            <el-button type="text" size="small" @click="deleteRow(scope.row)">删除</el-button>
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
    <el-dialog
      title="新增菜谱"
      :visible.sync="showAddMenu"
      width="300px"
    >
      <div style="height: 65px">
        <el-form ref="menuForm" style="width: 100%" :model="menuForm" :rules="menuRules" label-width="100px" class="demo-ruleForm">
          <el-form-item label="菜谱名称：" prop="name">
            <el-input v-model="menuForm.name" size="mini" />
          </el-form-item>
        </el-form>
      </div>
      <div style="text-align: center">
        <el-button size="mini" @click="cancel('menuForm')">取 消</el-button>
        <el-button size="mini" type="primary" @click="submitForm('menuForm')">提 交</el-button>
      </div>
    </el-dialog>
    <el-dialog
      title="编辑权限门店"
      :visible.sync="editLimit"
      width="1000px"
    >
      <set-limit :rowObj="rowObj" v-model="editLimit"></set-limit>
    </el-dialog>
  </div>
</template>

<script>
import setLimit from '@/views/business/dishes/menuList/components/setLimit'
export default {
  name: 'MenuList',
  components: {setLimit},
  data() {
    return {
      showAddMenu: false,
      menuForm: {
        name: ''
      },
      menuRules: {
        name: [
          { required: true, message: '请输入菜谱名称', trigger: 'blur' }
        ]
      },
      tableData: [
        { name: 1234, state: 0 },
        { name: 4567, state: 1 }
      ],
      multipleSelection: [],
      pageSize: 10,
      currentPage: 1,
      totalCells: 110,
      editLimit: false,
      rowObj: {}
    }
  },
  created() {
  },
  mounted() {
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          console.log(111)
          // this.showAddMenu = false
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    cancel(formName) {
      this.$refs[formName].resetFields()
      console.log(this.menuForm)
      this.showAddMenu = false
    },
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    addDishes() {
      this.showAddMenu = true
    },
    limitRow(row) {
      this.rowObj = row
      this.editLimit = true
    },
    deleteRow(row) {
      this.$confirm('此操作将永久删除该菜谱【' + row.name + '】, 是否继续?', '提示', {
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
