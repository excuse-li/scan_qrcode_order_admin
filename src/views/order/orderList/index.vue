<template>
  <div class="main-body">
    <div class="container">
      <div>
        <span>订单信息：</span>
        <el-input size="mini" placeholder="请输入桌台名称查询" style="width: 200px" v-model="searchKey" class="input-with-select">
          <el-button slot="append" icon="el-icon-search"></el-button>
        </el-input>
        <span style="margin-left: 20px;">门店信息：</span>
        <el-select size="mini" v-model="shop" style="width: 200px" placeholder="请选择所属门店">
          <el-option
            v-for="item in shops"
            :key="item.value"
            :label="item.name"
            :value="item.id">
          </el-option>
        </el-select>
        <span style="margin-left: 20px;">下单时间：</span>
        <el-date-picker
          size="mini"
          v-model="time"
          type="daterange"
          range-separator="至"
          start-placeholder="开始日期"
          end-placeholder="结束日期">
        </el-date-picker>
      </div>
      <div style="margin-top: 10px">
        <el-table
          :header-row-style="{
            'background-color': '#FAFAFA'
          }"
          size="mini"
          ref="multipleTable"
          :data="tableData"
          tooltip-effect="dark"
          style="width: 100%">
          <el-table-column
            type="selection"
            width="55">
          </el-table-column>
          <el-table-column
            prop="name"
            label="订单编号"
            min-width="120">
          </el-table-column>
          <el-table-column
            prop="name"
            label="下单门店"
            min-width="120">
          </el-table-column>
          <el-table-column
            prop=""
            label="订单来源"
            min-width="120">
          </el-table-column>
          <el-table-column
            prop=""
            label="订单金额"
            min-width="75">
          </el-table-column>
          <el-table-column
            prop=""
            label="支付方式"
            min-width="120">
          </el-table-column>
          <el-table-column
            prop=""
            label="下单时间"
            min-width="75">
          </el-table-column>
          <el-table-column
            fixed="right"
            label="操作"
            width="150"
            align="center">
            <template slot-scope="scope">
              <el-button
                @click.native.prevent="seeDetails(scope.row)"
                type="text"
                size="small">
                查看详情
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
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OrderList',
  data() {
    return {
      searchKey: '',
      shop: '',
      shops: [
        {id: 1, name: '门店1'},
        {id: 2, name: '门店2'},
        {id: 3, name: '门店3'},
        {id: 4, name: '门店4'}
      ],
      time: '',
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
    seeDetails(row) {
      this.$router.push({ path: '/order/orderDetails' })
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
