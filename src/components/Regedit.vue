<template>
  <div id="Regedit">
    <el-row type="flex" justify="center">
      <el-col span="8" >
        <!--注册表单-->
        <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" >
          <!--用户名-->
          <el-form-item label="用户名" prop="name">
            <el-input v-model="ruleForm.name" placeholder="请输入用户名"></el-input>
          </el-form-item>
          <!--密码-->
          <el-form-item label="密码" prop="password">
            <el-input v-model="ruleForm.password" type="password" placeholder="请输入密码"></el-input>
          </el-form-item>
          <!--确认密码-->
          <el-form-item label="确认密码" prop="passwordQualify">
            <el-input v-model="ruleForm.passwordQualify" type="password" placeholder="请再次输入密码"></el-input>
          </el-form-item>
          <!--手机号-->
          <el-form-item label="手机号" prop="mobileNumber">
            <el-input v-model="ruleForm.mobileNumber" maxlength=11></el-input>
          </el-form-item>
          <!--邮箱-->
          <el-form-item label="邮箱" prop="eMail">
            <el-input v-model="ruleForm.eMail" placeholder="请输入邮箱"></el-input>
          </el-form-item>
          <!--年龄-->
          <el-form-item label="年龄" prop="age">
            <el-input-number v-model="ruleForm.age" max=100 ></el-input-number>
          </el-form-item>
          <!--职称-->
          <el-form-item label="职称" prop="gender">
             <el-select v-model="ruleForm.gender" placeholder="请选择职称">
                <el-option
                      v-for="item in genderGroup"
                      :key="item.value"
                      :label="item.label"
                      :value="item.value">
                </el-option>
             </el-select>
          </el-form-item>
          <!--用户信息-->
          <el-form-item label="用户信息" prop="information">
            <el-input v-model="ruleForm.information" placeholder="请输入信息描述" type="textarea" autosize></el-input>
          </el-form-item>
          <!--按钮-->
          <el-form-item>
            <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
            <el-button @click="resetForm('ruleForm')">重置</el-button>
          </el-form-item>
        </el-form>
      </el-col>
    </el-row>

  </div>
</template>



<script>
    export default {
        name: "Regedit",
      data() {
        //自定义验证规则
        //密码验证
        var validatePass = (rule, value, callback) => {
          if (value === '') {
           callback(new Error('请再次输入密码'));
          } else if (value !== this.ruleForm.password) {
           callback(new Error('两次输入密码不一致!'));
          } else {
           callback();
          }
        };
        
        return {
          //职称集合
          genderGroup:[
            {value:'教授',label:'教授'},
            {value:'副教授',label:'副教授'},
            {value:'讲师',label:'讲师'}
          ],
          //表单数据初值
          ruleForm: {
            name:'',
            password:'',
            passwordQualify:'',
            mobileNumber:'',
            eMail:'',
            gender:'',
            age:30,
            information:''
          },
          //验证规则
          rules: {
            //用户名
            name: [
              { required: true, message: '请输入用户名', trigger: 'blur' },
              { min: 2, max: 5, message: '长度在 2 到 5 个字符', trigger: 'blur' }
            ],
            //密码
            password: [
              { required: true, message: '请输入密码', trigger: 'change' },
            ],
            //密码验证
            passwordQualify:[
              {  validator: validatePass ,trigger:['change','blur']}
            ],
            //年龄
            age: [
              { required: true, message: '请选择年龄', trigger: 'change' }
            ],
            //手机号
            mobileNumber:[
              {required:true, pattern:/^((1[3-8][0-9])+\d{8})$/,message:'请输入手机号',trigger:'change'},
            ],
            //邮箱
            eMail: [
              { type: 'email', required: true, message: '请输入邮箱', trigger: ['change','blur'] }
            ],
            //职称
            gender: [
              {required: true, message: '请选择一个职称', trigger: 'change' }
            ],
            //描述信息
            information: [
              { required: true, message: '请输入描述信息', trigger: 'change' }
            ],

          }
        };
      },
      methods: {
        submitForm(formName) {
          this.$refs[formName].validate((valid) => {
            if (valid) {
              alert('submit!');
            } else {
              console.log('error submit!!');
              return false;
            }
          });
        },
        resetForm(formName) {
          this.$refs[formName].resetFields();
        }
      }

    }
</script>

<style scoped>

</style>
