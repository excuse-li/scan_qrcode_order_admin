<template>
  <div class="main-body">
    <div class="container">
      <div class="form-container">
        <el-form ref="staffForm" style="margin-top: 35px" :model="staffForm" :rules="staffRules" label-width="100px" class="demo-ruleForm">
          <el-form-item label="员工头像：">
            <el-upload
              class="avatar-uploader"
              action="https://jsonplaceholder.typicode.com/posts/"
              :show-file-list="false"
              :on-success="handleAvatarSuccess"
              :before-upload="beforeAvatarUpload"
            >
              <img v-if="staffForm.imageUrl" :src="staffForm.imageUrl" class="avatar">
              <i v-else class="el-icon-plus avatar-uploader-icon" />
            </el-upload>
          </el-form-item>
          <el-form-item label="员工姓名：" prop="name">
            <el-input v-model="staffForm.name" placeholder="请输员工姓名" />
          </el-form-item>
          <el-form-item label="员工性别：" prop="sex">
            <el-radio-group v-model="staffForm.sex">
              <el-radio label="男" />
              <el-radio label="女" />
            </el-radio-group>
          </el-form-item>
          <el-form-item label="联系电话：" prop="phone">
            <el-input v-model="staffForm.phone" placeholder="请输入联系电话" />
          </el-form-item>
          <el-form-item label="所属门店：" prop="shop">
            <el-select style="width: 100%" v-model="staffForm.shop" placeholder="请选择">
              <el-option
                v-for="item in shopArr"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              />
            </el-select>
          </el-form-item>
          <el-form-item label="员工角色：" prop="role">
            <el-select style="width: 100%" v-model="staffForm.role" placeholder="请选择">
              <el-option
                v-for="item in roleArr"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              />
            </el-select>
          </el-form-item>
        </el-form>
        <div style="text-align: center">
          <el-button @click="cancel('staffForm')">取 消</el-button>
          <el-button type="primary" @click="submitForm('staffForm')">提 交</el-button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AddStaff',
  data() {
    return {
      shopArr: [
        {
          value: 0,
          label: '门店1'
        }, {
          value: 1,
          label: '门店2'
        }, {
          value: 2,
          label: '门店3'
        }
      ],
      roleArr: [
        {
          value: 0,
          label: '超级管理员'
        }, {
          value: 1,
          label: '管理员'
        }, {
          value: 2,
          label: '普通用户'
        }
      ],
      staffForm: {
        name: '',
        sex: '',
        shop: '',
        role: '',
        imageUrl: '',
        phone: ''
      },
      staffRules: {
        name: [
          { required: true, message: '请输入门店名称', trigger: 'blur' }
        ],
        sex: [
          { required: true, message: '请选择员工性别', trigger: 'change' }
        ],
        shop: [
          { required: true, message: '请选择所属门店', trigger: 'change' }
        ],
        phone: [
          { required: true, message: '请输入联系电话', trigger: 'blur' }
        ]
      },
      cityOptions: [
        {
          value: 'zhinan',
          label: '指南',
          children: [{
            value: 'shejiyuanze',
            label: '设计原则',
            children: [{
              value: 'yizhi',
              label: '一致'
            }, {
              value: 'fankui',
              label: '反馈'
            }, {
              value: 'xiaolv',
              label: '效率'
            }, {
              value: 'kekong',
              label: '可控'
            }]
          }, {
            value: 'daohang',
            label: '导航',
            children: [{
              value: 'cexiangdaohang',
              label: '侧向导航'
            }, {
              value: 'dingbudaohang',
              label: '顶部导航'
            }]
          }]
        }, {
          value: 'zujian',
          label: '组件',
          children: [{
            value: 'basic',
            label: 'Basic',
            children: [{
              value: 'layout',
              label: 'Layout 布局'
            }, {
              value: 'color',
              label: 'Color 色彩'
            }, {
              value: 'typography',
              label: 'Typography 字体'
            }, {
              value: 'icon',
              label: 'Icon 图标'
            }, {
              value: 'button',
              label: 'Button 按钮'
            }]
          }]
        }
      ]
    }
  },
  created() {
  },
  mounted() {
  },
  methods: {
    handleAvatarSuccess(res, file) {
      this.imageUrl = URL.createObjectURL(file.raw)
    },
    beforeAvatarUpload(file) {
      const isJPG = file.type === 'image/jpeg'
      const isLt2M = file.size / 1024 / 1024 < 2

      if (!isJPG) {
        this.$message.error('上传头像图片只能是 JPG 格式!')
      }
      if (!isLt2M) {
        this.$message.error('上传头像图片大小不能超过 2MB!')
      }
      return isJPG && isLt2M
    },
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
      this.$router.push({ path: '/shop/staffList' })
    }
  }
}
</script>

<style scoped>

</style>
<style>
  .avatar-uploader .el-upload {
    border: 1px dashed #d9d9d9;
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }
  .avatar-uploader .el-upload:hover {
    border-color: #409EFF;
  }
  .avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    line-height: 178px;
    text-align: center;
  }
  .avatar {
    width: 178px;
    height: 178px;
    display: block;
  }
</style>
