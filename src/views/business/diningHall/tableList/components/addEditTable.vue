<template>
  <div>
    <el-form ref="tableForm" style="width: 95%" :model="tableForm" :rules="tableRules" label-width="120px" class="demo-ruleForm">
      <el-form-item label="选择门店：" prop="shop">
        <el-select size="mini" style="width: 100%" v-model="tableForm.shop" placeholder="请选择所属门店">
          <el-option
            v-for="item in shops"
            :key="item.value"
            :label="item.name"
            :value="item.id">
          </el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="添加桌号：" prop="number">
        <el-input
          type="textarea"
          :rows="2"
          placeholder="例：A01，A02，荷花亭"
          v-model="tableForm.number">
        </el-input>
      </el-form-item>
      <el-form-item label="">
        <div style="color: rgba(0, 0, 0, 0.25);line-height: 20px;font-size: 12px;">
          <span>输入您需要添加的桌号，并通过“，”进行分割；数字、字母、汉字不限，不支持特殊字符</span>
        </div>
      </el-form-item>
    </el-form>
    <div style="width: 95%;text-align: right">
      <el-button size="mini" @click="cancel('staffForm')">取 消</el-button>
      <el-button size="mini" type="primary" @click="submitForm('tableForm')">提 交</el-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AddEditTable',
  model: {
    prop: 'addEditTableShow',
    event: 'change'
  },
  props: {
    addEdit: Object,
    default: null
  },
  data() {
    return {
      shops: [],
      tableForm: {
        shop: '',
        number: ''
      },
      tableRules: {
        shop: [
          { required: true, message: '请选择所属门店', trigger: 'change' }
        ],
        number: [
          { required: true, message: '请输入桌号', trigger: 'blur' }
        ]
      }
    }
  },
  created() {
    console.log(this.addEdit)
  },
  mounted() {
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.$emit('getFatherData')
          this.$emit('change', false)
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    cancel(formName) {
      this.$emit('change', false)
    }
  }
}
</script>

<style scoped>

</style>
