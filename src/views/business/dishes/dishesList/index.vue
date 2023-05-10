<template>
  <div>
    <div>
      <span>菜品名称：</span>
      <el-input v-model="searchKey" size="mini" placeholder="请输入菜品名称查询" style="width: 200px" class="input-with-select">
        <el-button slot="append" icon="el-icon-search" />
      </el-input>
      <span style="margin-left: 20px;">菜品类型：</span>
      <el-select v-model="type" size="mini" style="width: 200px" placeholder="请选择菜品类型">
        <el-option
          v-for="item in types"
          :key="item.value"
          :label="item.name"
          :value="item.id"
        />
      </el-select>
    </div>
    <div class="dishes-body">
      <div class="dishes-left">
        <div class="div-border">
          <div style="height: 50px;margin: 0 10px">
            <div style="float: left;height: 50px;line-height: 50px">
              <span>菜品分类</span>
            </div>
            <div style="float: right;height: 50px;line-height: 50px">
              <el-button size="mini" type="primary" plain icon="el-icon-plus">分类</el-button>
            </div>
          </div>
          <div v-for="(item, index) in kinds" :key="item.index" style="cursor: pointer" :class="active === index ? 'active-select' : 'no-select'" @click="selectItem(item, index)">
            <div :style="active === index ? '' : 'border-bottom: 1px solid #e8e8e8;'" class="kind-item">
              <div class="item-left">
                <span>{{ item.name }}({{ item.total }})</span>
              </div>
              <div class="item-right" style="color: #ffffff">
                <el-button type="text" size="small" @click.native.prevent="addItem(item)">
                  <span :style="active === index ? 'color: #ffffff' : ''">加菜</span>
                </el-button>
                <el-button type="text" size="small" @click.native.prevent="deleteItem(item)">
                  <span :style="active === index ? 'color: #ffffff' : ''">删除</span>
                </el-button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="dishes-right">
        <el-table
          ref="multipleTable"
          :header-row-style="{
            'background-color': '#FAFAFA'
          }"
          size="mini"
          :data="tableData"
          tooltip-effect="dark"
          style="width: 100%;margin-top: 10px"
        >
          <el-table-column
            prop="name"
            label="菜品名称"
            min-width="120"
          />
          <el-table-column
            prop="name"
            label="菜品类型"
            min-width="120"
          />
          <el-table-column
            prop=""
            label="售价"
            min-width="120"
          />
          <el-table-column
            fixed="right"
            label="操作"
            width="150"
            align="center"
          >
            <template slot-scope="scope">
              <el-button
                type="text"
                size="small"
                @click.native.prevent="editRow(scope.row)"
              >
                编辑
              </el-button>
              <el-button
                type="text"
                size="small"
                @click.native.prevent="deleteRow(scope.row)"
              >
                删除
              </el-button>
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
      </div>
    </div>
    <el-dialog
      title="从菜品库中选择菜品"
      :visible.sync="showAddDishes"
      width="1000px"
    >
      <add-dishes :typeObj="addObj" v-model="showAddDishes"></add-dishes>
    </el-dialog>
  </div>
</template>

<script>
import addDishes from '@/views/business/dishes/dishesList/components/addDishes'
export default {
  name: 'DishesList',
  components: {addDishes},
  data() {
    return {
      searchKey: '',
      type: '',
      types: [],
      // 左边
      active: 0,
      kinds: [
        { name: '分类1', total: 256 },
        { name: '分类2', total: 256 },
        { name: '分类3', total: 256 },
        { name: '分类4', total: 256 },
        { name: '分类5', total: 256 },
        { name: '分类6', total: 256 },
        { name: '分类7', total: 256 },
        { name: '分类8', total: 256 },
        { name: '分类9', total: 256 },
        { name: '分类10', total: 256 },
        { name: '分类11', total: 256 },
        { name: '分类12', total: 256 }
      ],
      showAddDishes: false,
      addObj: {},
      // 右边
      tableData: [
        {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-02',
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
  methods: {
    selectItem(item, index) {
      console.log(item)
      this.active = index
    },
    addItem(item) {
      this.addObj = item
      this.showAddDishes = true
    },
    deleteItem(item) {
      this.$confirm('此操作将永久删除该分类【' + item.name + '】, 是否继续?', '提示', {
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
    editRow(row) {},
    deleteRow(row) {
      this.$confirm('此操作将永久删除该菜品【' + row.name + '】, 是否继续?', '提示', {
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
.dishes-body{
  height: calc(100vh - 150px);
  margin-top: 10px;
}
.dishes-left{
  float: left;
  width: 300px;
  height: 100%;
  /*overflow-y: auto;*/
}
.div-border{
  margin: 10px;
  border-radius: 8px;
  border: 1px solid #979797;
  height: calc(100vh - 170px);
  overflow-y: auto;
}
.active-select{
  background-color: #1890FF;
  color: #ffffff;
}
.no-select{
  color: rgba(0, 0, 0, 0.65);
}
.kind-item{
  height: 40px;
  margin: 0 10px;
  /*border-bottom: 1px solid #e8e8e8;*/
}
.item-left{
  float: left;
  width: 170px;
  height: 40px;
  line-height: 40px;
}
.item-right{
  float: right;
  width: 70px;
  height: 40px;
  line-height: 40px;
}
.dishes-right{
  float: left;
  width: calc(100% - 300px);
  height: 100%;
  overflow-y: auto;
}
</style>
