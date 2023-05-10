<template>
  <div class="main-body">
    <div class="container">
      <div style="height: 40px;line-height: 30px;">
        <strong>基本信息</strong>
      </div>
      <div style="color: rgba(0, 0, 0, 0.85);font-size: 14px">
        <div style="height: 30px">
          <el-row>
            <el-col :span="8">
              <span>订单编号：</span>
              <span>{{orderId}}</span>
            </el-col>
            <el-col :span="8">
              <span>下单门店：</span>
              <span>{{orderShop}}</span>
            </el-col>
            <el-col :span="8">
              <span>订单来源：</span>
              <span>{{orderSource}}</span>
            </el-col>
          </el-row>
        </div>
        <div style="height: 30px">
          <span>下单时间：</span>
          <span>{{orderTime}}</span>
        </div>
      </div>
      <div class="line-hr"></div>
      <div style="height: 40px;line-height: 30px;margin-top: 15px">
        <strong>支付信息</strong>
      </div>
      <div style="color: rgba(0, 0, 0, 0.85);font-size: 14px">
        <div style="height: 30px">
          <el-row>
            <el-col :span="8">
              <span>订单金额：</span>
              <span>¥{{payOrder}}</span>
            </el-col>
            <el-col :span="8">
              <span>实际支付：</span>
              <span>¥{{endPay}}</span>
            </el-col>
            <el-col :span="8">
              <span>支付方式：</span>
              <span>{{orderWay}}</span>
            </el-col>
          </el-row>
        </div>
        <div style="height: 30px">
          <span>支付时间：</span>
          <span>{{payTime}}</span>
        </div>
      </div>
      <div class="line-hr"></div>
      <div style="height: 40px;line-height: 30px;margin-top: 15px">
        <strong>商品信息</strong>
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
          show-summary
          :summary-method="getSummaries">
          <el-table-column
            prop="name"
            label="商品名称"
            min-width="120">
          </el-table-column>
          <el-table-column
            prop="amount1"
            label="单价"
            min-width="70">
          </el-table-column>
          <el-table-column
            prop="amount3"
            label="数量"
            min-width="70">
          </el-table-column>
          <el-table-column
            prop=""
            label="总金额"
            min-width="100">
          </el-table-column>
        </el-table>
      </div>
<!--      <div style="text-align: center">-->
<!--        <el-button type="primary" @click="back()">返 回</el-button>-->
<!--      </div>-->
    </div>
  </div>
</template>

<script>
export default {
  name: 'OrderDetails',
  data() {
    return {
      orderId: '35265',
      orderShop: '南山门店',
      orderSource: '扫码点餐',
      orderTime: '2021-01-25 20:00:00',
      payOrder: '2545',
      endPay: '2545',
      orderWay: '微信支付',
      payTime: '2021.01-25 22:00:00',
      tableData: [
        {
          id: '12987123',
          name: '王小虎',
          amount1: '165',
          amount2: '4.43',
          amount3: 12
        }
      ]
    }
  },
  created() {
  },
  mounted() {
  },
  methods: {
    getSummaries(param) {
      const { columns, data } = param
      const sums = []
      columns.forEach((column, index) => {
        if (index === 0) {
          sums[index] = '总价'
          return
        }
        const values = data.map(item => Number(item[column.property]))
        if (!values.every(value => isNaN(value))) {
          sums[index] = values.reduce((prev, curr) => {
            const value = Number(curr)
            if (!isNaN(value)) {
              return prev + curr
            } else {
              return prev
            }
          }, 0)
          sums[index] += ' 元'
        } else {
          sums[index] = ''
        }
      })
      return sums
    },
    back() {
      this.$router.push({ path: '/order/order' })
    }
  }
}
</script>

<style scoped>
.line-hr{
  height: 1px;
  background: #E8E8E8;
}
</style>
