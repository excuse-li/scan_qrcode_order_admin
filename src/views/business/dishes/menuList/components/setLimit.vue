<template>
  <div style="margin-top: -20px">
    <div class="dishes-body">
      <div class="dishes-left">
        <div class="top-line">
          <el-input
            size="mini"
            style="width: 250px"
            placeholder="请输入城市名称"
            suffix-icon="el-icon-search"
            v-model="name">
          </el-input>
        </div>
        <div style="margin: 10px 15px">
          <el-tag size="mini">城市</el-tag>
        </div>
      </div>
      <div class="dishes-right">
        <div class="top-line">
          <el-input
            size="mini"
            style="width: 250px"
            placeholder="请输入门店"
            suffix-icon="el-icon-search"
            v-model="name">
          </el-input>
        </div>
        <el-table
          ref="multipleTable"
          style="width: 100%;margin-top: 10px"
          :header-row-style="{
        'background-color': '#FAFAFA'
      }"
          size="mini"
          :data="tableData"
          tooltip-effect="dark"
          @selection-change="handleSelectionChange"
        >
          <el-table-column
            type="selection"
            width="55"
          />
          <el-table-column
            prop="name"
            label="门店"
          />
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
      </div>
    </div>
    <div style="text-align: right;margin-top: 10px">
      <el-button size="mini" @click="cancel()">取 消</el-button>
      <el-button size="mini" type="primary" @click="submitForm()">提 交</el-button>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'setLimit',
    props: {
      rowObj: Object,
      default: null
    },
    model: {
      prop: 'editLimit',
      event: 'change'
    },
    data() {
      return {
        name: '',
        tableData: [
          { name: 1234, state: 0 },
          { name: 4567, state: 1 }
        ],
        multipleSelection: [],
        pageSize: 10,
        currentPage: 1,
        totalCells: 150
      }
    },
    created() {
      console.log(this.rowObj)
    },
    methods: {
      handleSelectionChange(val) {
        this.multipleSelection = val
      },
      handleSizeChange(val) {
        console.log(`每页 ${val} 条`)
      },
      handleCurrentChange(val) {
        console.log(`当前页: ${val}`)
      },
      submitForm() {
      },
      cancel() {
        this.$emit('change', false)
      }
    }
  }
</script>

<style scoped>
  .dishes-body{
    height: 400px;
    border: 1px solid #e6e2e2;
    border-radius: 8px;
  }
  .dishes-left{
    float: left;
    width: 280px;
    border-right: 1px solid #e6e2e2;
    overflow-y: auto;
    height: 100%;
  }
  .dishes-right{
    float: left;
    width: calc(100% - 280px);
    overflow-y: auto;
    height: 100%;
  }
  .top-line{
    height: 50px;
    line-height: 50px;
    border-bottom: 1px solid #e6e2e2;
    padding-left: 15px;
  }
</style>
