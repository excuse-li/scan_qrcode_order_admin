<template>
  <div class="main-body">
    <div class="container">
      <div class="form-container">
        <el-form :model="shopForm" :rules="shopRules" ref="shopForm" label-width="100px" class="demo-ruleForm">
          <div style="height: 50px;line-height: 50px">
            <strong>基本信息</strong>
          </div>
          <el-form-item label="门店名称：" prop="name">
            <el-input placeholder="请输入门店名称" v-model="shopForm.name"></el-input>
          </el-form-item>
          <el-form-item label="所在城市：" prop="city">
            <el-cascader
              style="width: 100%"
              v-model="shopForm.city"
              placeholder="请选择省/市/区"
              :options="cityOptions"
              :props="{ checkStrictly: true }"
              clearable></el-cascader>
          </el-form-item>
          <el-form-item label="详细地址：" prop="address">
            <el-input
              placeholder="请输入门店的详细地址"
              type="textarea"
              :rows="2"
              v-model="shopForm.address" />
          </el-form-item>
          <el-form-item label="位置标记：" prop="mapaddress">
            <el-input placeholder="请搜索地址" v-model="shopForm.mapaddress" class="input-with-select">
              <el-button slot="append" icon="el-icon-search"></el-button>
            </el-input>
          </el-form-item>
          <div style="height: 220px">
            地图
          </div>
          <div style="height: 50px;line-height: 50px">
            <strong>服务信息</strong>
          </div>
          <el-form-item label="门店图片：">
            <el-upload
              class="avatar-uploader"
              action="https://jsonplaceholder.typicode.com/posts/"
              :show-file-list="false"
              :on-success="handleAvatarSuccess"
              :before-upload="beforeAvatarUpload">
              <img v-if="shopForm.imageUrl" :src="shopForm.imageUrl" class="avatar">
              <i v-else class="el-icon-plus avatar-uploader-icon"></i>
            </el-upload>
          </el-form-item>
          <el-form-item label="门店介绍：">
            <el-input
              placeholder="请输入门店介绍"
              type="textarea"
              :rows="2"
              v-model="shopForm.introducer" />
          </el-form-item>
          <el-form-item label="联系电话：" prop="phone">
            <el-input placeholder="请输入联系电话" v-model="shopForm.phone"></el-input>
          </el-form-item>
        </el-form>
        <div style="text-align: center">
          <el-button @click="cancel('shopForm')">取 消</el-button>
          <el-button type="primary" @click="submitForm('shopForm')">提 交</el-button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'EditShop',
  data() {
    return {
      shopForm: {
        name: '',
        city: '',
        address: '',
        mapaddress: '',
        imageUrl: '',
        introducer: '',
        phone: ''
      },
      shopRules: {
        name: [
          { required: true, message: '请输入门店名称', trigger: 'blur' }
        ],
        city: [
          { required: true, message: '请选择所在地区', trigger: 'change' }
        ],
        address: [
          { required: true, message: '请输入详细地址', trigger: 'blur' }
        ],
        mapaddress: [
          { required: true, message: '请输标记位置', trigger: 'blur' }
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
      this.imageUrl = URL.createObjectURL(file.raw);
    },
    beforeAvatarUpload(file) {
      const isJPG = file.type === 'image/jpeg';
      const isLt2M = file.size / 1024 / 1024 < 2;

      if (!isJPG) {
        this.$message.error('上传头像图片只能是 JPG 格式!');
      }
      if (!isLt2M) {
        this.$message.error('上传头像图片大小不能超过 2MB!');
      }
      return isJPG && isLt2M;
    },
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('submit!');
        } else {
          console.log('error submit!!')
          return false;
        }
      })
    },
    cancel(formName) {
      this.$refs[formName].resetFields()
      this.$router.push({path: '/shop/shopList'})
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
