<template>
  <div class="main-body">
    <div class="container">
      <div class="form-container">
        <el-form ref="printerForm" style="margin-top: 35px" :model="printerForm" :rules="printerRules" label-width="140px" class="demo-ruleForm">
          <div style="height: 50px;line-height: 50px">
            <strong>基本信息</strong>
          </div>
          <el-form-item label="设备名称：" prop="name">
            <el-input v-model="printerForm.name" placeholder="请输入设备名称" />
          </el-form-item>
          <el-form-item label="打印机类型：" prop="type">
            <el-radio-group v-model="printerForm.type">
              <el-radio label="云打印机：" />
            </el-radio-group>
          </el-form-item>
          <el-form-item label="设备品牌：" prop="brand">
            <el-radio-group v-model="printerForm.brand">
              <el-radio label="云打印机：" />
            </el-radio-group>
          </el-form-item>
          <el-form-item label="设备SN号：" prop="sn">
            <el-input v-model="printerForm.sn" placeholder="请输入设备SN号" />
          </el-form-item>
          <el-form-item label="设备Key：" prop="key">
            <el-input v-model="printerForm.key" placeholder="请输入设备Key" />
          </el-form-item>
          <el-form-item label="打印小票规格：" prop="size">
            <el-radio-group v-model="printerForm.size">
              <el-radio label="80mm" />
              <el-radio label="55mm" />
            </el-radio-group>
          </el-form-item>
        </el-form>
        <div style="text-align: center">
          <el-button @click="cancel('printerForm')">取 消</el-button>
          <el-button type="primary" @click="submitForm('printerForm')">提 交</el-button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'EditPrinter',
  data() {
    return {
      printerForm: {
        name: '',
        type: '',
        brand: '',
        sn: '',
        key: '',
        size: ''
      },
      printerRules: {
        name: [
          { required: true, message: '请输入门店名称', trigger: 'blur' }
        ],
        type: [
          { required: true, message: '请选择设备类型', trigger: 'change' }
        ],
        brand: [
          { required: true, message: '请选择设备品牌', trigger: 'change' }
        ],
        sn: [
          { required: true, message: '请输入设备SN号', trigger: 'blur' }
        ],
        key: [
          { required: true, message: '请输入设备Key', trigger: 'blur' }
        ],
        size: [
          { required: true, message: '请选择打印小票规格', trigger: 'change' }
        ],
        shop: [
          { required: true, message: '请选择所属门店', trigger: 'change' }
        ],
        phone: [
          { required: true, message: '请输入联系电话', trigger: 'blur' }
        ]
      }
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
          alert('submit!')
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    cancel(formName) {
      this.$refs[formName].resetFields()
      this.$router.push({ path: '/shop/printerList' })
    }
  }
}
</script>

<style scoped>

</style>
