<template>
  <div class="main-body">
    <div class="container">
      <div>
        <span>员工查询：</span>
        <el-input size="mini" placeholder="请输入内容" style="width: 200px" v-model="searchKey" class="input-with-select">
          <el-button slot="append" icon="el-icon-search"></el-button>
        </el-input>
        <span style="margin-left: 20px;">所在城市：</span>
        <el-select size="mini" v-model="city" style="width: 200px" placeholder="请选择门店所在城市">
          <el-option
            v-for="item in citys"
            :key="item.value"
            :label="item.name"
            :value="item.id">
          </el-option>
        </el-select>
      </div>
      <div style="margin: 10px 0">
        <el-button size="mini" type="primary" icon="el-icon-plus" @click="toAddStaff">添加员工</el-button>
        <el-select
          size="mini"
          v-model="set"
          multiple
          collapse-tags
          style="margin-left: 20px;"
          placeholder="批量操作">
          <el-option
            v-for="item in setArr"
            :key="item.value"
            :label="item.label"
            :value="item.value">
          </el-option>
        </el-select>
      </div>
      <div>
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
            label="门店ID"
            width="120">
            <template slot-scope="scope">{{ scope.row.date }}</template>
          </el-table-column>
          <el-table-column
            prop="name"
            label="门店名称"
            width="120">
          </el-table-column>
          <el-table-column
            prop="name"
            label="门店状态">
          </el-table-column>
          <el-table-column
            prop="address"
            label="地址"
            show-overflow-tooltip>
          </el-table-column>
          <el-table-column
            fixed="right"
            label="操作"
            width="120"
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
  <!--      <div style="margin-top: 20px">-->
  <!--        <el-button @click="toggleSelection([tableData[1], tableData[2]])">切换第二、第三行的选中状态</el-button>-->
  <!--        <el-button @click="toggleSelection()">取消选择</el-button>-->
  <!--      </div>-->
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'staffList',
    data () {
      return {
        searchKey: '',
        city: '',
        citys: [
          {id: 1, name: '北京'},
          {id: 2, name: '上海'},
          {id: 3, name: '广州'},
          {id: 4, name: '深圳'}
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
        totalCells: 110
      }
    },
    created() {
    },
    mounted() {
    },
    methods: {
      toAddStaff(){
        this.$router.push({path: '/shop/addStaff'})
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
      stateRow(item) {},
      editRow(row) {
        this.$router.push({path: '/shop/editStaff'})
      },
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
