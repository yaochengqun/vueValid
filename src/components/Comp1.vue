<template>
	<div class="comp1">
    <el-row>
      <el-col :span="24">24</el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="16">16</el-col>
      <el-col :span="8">8</el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="16"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="16"><div class="grid-content bg-purple"></div></el-col>
      <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
    </el-row>

		<el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px">
			<el-form-item label="用户名" prop="name">
				<el-input v-model="ruleForm.name"></el-input>
			</el-form-item>
			<el-form-item label="密码" prop="pwd">
				<el-input v-model="ruleForm.pwd" type="password"></el-input>
			</el-form-item>
			<el-form-item label="重复密码" prop="repwd">
				<el-input v-model="ruleForm.repwd" type="password"></el-input>
			</el-form-item>
      <el-form-item label="URL" prop="url">
        <el-input v-model="ruleForm.url"></el-input>
      </el-form-item>
      <el-form-item label="E-mail" prop="email">
        <el-input v-model="ruleForm.email"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>
        <el-button type="primary" @click="resetForm('ruleForm')">重置</el-button>
      </el-form-item>
		</el-form>
	</div>
</template>

<script>
export default {
	name: 'Comp1',
	data(){
		var validatePass = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入密码'));
      } else {
        if (this.ruleForm.repwd !== '') {
          this.$refs.ruleForm.validateField('repwd');
        }
        callback();
      }
    };
    var validatePass2 = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请再次输入密码'));
      } else if (value !== this.ruleForm.pwd) {
        callback(new Error('两次输入密码不一致!'));
      } else {
        callback();
      }
    };
		return {
			ruleForm:{
				name:"",
				pwd:"",
				repwd:"",
        url:"",
        email:""
			},
			rules:{
				name:[
					{
						required:true,
						message:"请输入用户名",
						trigger:"blur"
					},
					{
						min:3,
						max:6,
						message:"长度在3到5个字符",
						trigger:"blur"
					}
				],
				pwd:[
          {
            required:true,
            message:"请输入密码"
          },
          {
            min:6,
            max:16,
            message:"输入6-16个字符",
            trigger:"blur"
          },
          {
            validator:validatePass,
            trigger:"blur"
          }
				],
				repwd:[
          {
            validator:validatePass2,
            trigger:"blur"
          }
				],
        url:[
          {
            type:"url",
            message:"请输入正确的url格式"
          }
        ],
        email:[
          {
            type:"email",
            message:"请输入正确的E-mail格式"
          }
        ]
			}
		}
	},
  methods:{
    submitForm(formName){
      this.$refs[formName].validate((valid) => {
        if(valid){
          alert("提交成功！");
        }else{
          return false;
        }
      })
    },
    resetForm(formName){
      this.$refs[formName].resetFields();
    }
  }
}
</script>

<style scoped>
.el-row {
    margin-bottom: 20px;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
</style>