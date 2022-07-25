
 <template>
  
  <div> 
    
     <div style="box-sizing:border-box;padding-left:250px">
    <h-steps :current="current" style="margin-bottom: 12px;">
      <h-step  > <h3 class="stepWords">基本信息</h3>   </h-step>
      <h-step  > <h3 class="stepWords">风险评级</h3></h-step>
      <h-step  > <h3 style=" margin-left:-23px">银行卡信息</h3></h-step>
    </h-steps>
    </div>
   
        
     <h-collapse >

    
      <div>
    <h-form
      ref="formValidate"
      :model="formValidate"
      :rules="ruleValidate"
      :label-width="180"
    >


    <!-- 姓名 -->
      <div class="needcenter">
      <h-form-item   prop="name" >
        <span slot="label" class="inputsLabel">
      	  <span>客户姓名</span>
          </span>
          <h-col span="10">
        <h-input v-model="formValidate.name"  
         :maxlength="15"
        placeholder="请输入姓名" size="large" col="15" ></h-input>
          </h-col>
      </h-form-item>
      </div>
       
        

 
       <!-- 性别 -->
      <div class="needcenter">
      <h-form-item  prop="gender" size="large">
          <span slot="label" class="inputsLabel">
      	  <span>性别</span>
          </span>
        <h-radio-group v-model="formValidate.gender">
          <h-radio label="male">
      	  <span class="inputsLabel" style="font-weight:bold">男</span>
           
          </h-radio>
          <h-radio label="female">
      	  <span class="inputsLabel" style="font-weight:bold">女</span>

          </h-radio>
        </h-radio-group>
      </h-form-item>
      </div>
   

    <!-- 客户类型 -->
      <div class="needcenter">
      <h-form-item prop="client_type">
        <span slot="label" class="inputsLabel">
      	  <span>客户类型</span>
          </span>
          <h-col span="10">
            <h-select v-model="formValidate.client_type" placeholder="请选择用户类型" size="large">
              
              <h-option value="only">个体户</h-option>
              <h-option value="many">集体户</h-option>
              
            </h-select>
          </h-col>
      </h-form-item>
      </div>


    <!-- 身份证类型 -->
      <div class="needcenter">
      <h-form-item prop="credentials_type">
         <span slot="label" class="inputsLabel">
      	  <span>证件类型</span>
          </span>
          <h-col span="10">
            <h-select v-model="formValidate.credentials_type"  placeholder="请选择身份证类型" size="large">
              <h-option value="land">大陆身份证</h-option>
              <h-option value="non_land">港澳台通行证</h-option>
              
            </h-select>
        </h-col>
      </h-form-item>
      </div>


       <!-- 身份证号码 -->
      <div class="needcenter">
      <h-form-item  prop="credentials">
        <span slot="label" class="inputsLabel">
      	  <span>身份证号码</span>
          </span>
          <h-col span="10">
             <h-input v-model="formValidate.credentials" :maxlength="15" placeholder="请输入身份证号码" size="large"></h-input>
          </h-col>
      </h-form-item>
      </div>
      
       
      <h-form-item>

         <router-link to="/user2">
        <h-button type="primary" @click="handleSubmit('formValidate')"
          style="margin-left:350px">
      	  <span class="inputsLabel" style="font-weight:bold">下一步</span>
          </h-button>
        </router-link>

        

      </h-form-item>
    </h-form>
  </div>

 
    </h-collapse>
  </div>
 
    
</template>


<script>
   
   export default {
       //...
methods: {
	//...
	inputLimit(val) {
		// 正则匹配非中英文及数字的字符
		let reg = /[^\u4e00-\u9fa5a-zA-Z0-9]/;
		// 查找是否有非中英文及数字的字符
		// 没有则返回-1，有则返回对应位置
		let n = val.search(reg);
		if ( n !== -1 ) {
		    // 由于每次触发，通常只有最后一个字符是有可能异常的
		    // 所以这里是直接截取异常字符前面的部分
			this.value = val.slice(0, n);
		}
	}
},

//...



 

    data() {
    return {
      current: 0,//步骤条走到哪一步
     formValidate: {
        name: "",
        credentials: "",
        client_type: "",
        gender: "",
        credentials_type:""
        
      },
      ruleValidate: {
        name: [{ required: true, message: "姓名不能为空", trigger: "blur" }],
        credentials: [
          { required: true, message: "身份证号码不能为空", trigger: "blur" },
           
        ],
        client_type: [{ required: true, message: "请选择客户类型", trigger: "blur" }],
        credentials_type: [{ required: true, message: "请选择身份证类型", trigger: "blur" }],
        gender: [{ required: true, message: "请选择性别", trigger: "blur" }],
         
      },
    };

  
  },
  
    handleSubmit(name) {
      this.$refs[name].validate((valid) => {
        if (valid) {
          this.$hMessage.success("提交成功!");
        } else {
          this.$hMessage.error("表单验证失败!");
        }
      });
    },
    handleReset(name) {
      this.$refs[name].resetFields();
    },
    	validateTag: function () {
			var reg = /^[\u0391-\uFFE5A-Za-z]+$/;
			if (reg.test(this.newData.tagTitle)) {
				this.errorTips = false;
			} else {
				this.errorTips = true
			}
		}
    
    

  };
  
</script>


<style lang="less" scoped>
  .needcenter {//输入框的位置
     margin-left: 250px;
     margin-top: 30px;
 
    }
    .stepWords{//改变步骤条下面文字的位置
  margin-left:-15px
     }
     .inputsLabel{//改变输入框旁边文字的大小和位置
  
          font-size: 150%;
      //  font-weight:bold;
          opacity:90% //字体颜色调浅一些
}
 
</style>


