<template>
  <div>
	<myheader></myheader>

	<section class="featured-block text-center">
		<div class="container">
			<!-- 头部 -->
			<div>

				<Breadcrumb :datas='datas'></Breadcrumb>

			</div>

			<!-- 表单 -->
			<div>

				<table>

					<tr>
						<td>
							用户名：
						</td>
						<td>
							<input type="text" v-model='username''>
						</td>
					</tr>

					<tr>
						<td>
							密码：
						</td>
						<td>
							<input type="password" v-model='password'>
						</td>
					</tr>
					<tr>
						<td>
							手机号：
						</td>
						<td>
							<input type="text" v-model='phone'>
						</td>
					</tr>

					<tr>
						<td></td>
						<td>
							<Button color='blue' @click='submit'>提交</Button>
						</td>
					</tr>

				</table>

			</div>



		</div>
	</section>
	

	
	
	
	<footer class="footer">

		<div class="container">
			@v3u.cn
		</div>
		
		
	</footer>
    
  </div>
  
</template>


 
<script>

// 导入组件
import myheader from './myheader.vue'

export default {
  data () {
    return {
	  msg: "这是一个变量",

	  // 面包屑导航变量
	  datas:[{title:'首页',route:{name:'index'}},{title:'注册页面'}],

	  // 表单数据
	  username :'',
	  password :'',
	  phone:'',
	
    }
  },

  // 注册组件标签
  components:{
	  'myheader':myheader
  },

  mounted:function(){

	


	},
  methods:{

	// 定义提交事件
	submit:function(){

		// 非空验证
		if (this.username==''){

			this.$Message('您没有输入用户名');
			return false

		}
		else if(this.password == ''){

			this.$Message('您没有输入密码');
			return false

		}

		// 请求后台接口
		this.axios.get('http://localhost:8000/register/',{params:{
			username:this.username,password:this.password,phone:this.phone
		}}).then((result)=>{

			console.log(result);

			this.$Message(result.data.message);

			this.password = '';

		});

	}

     
  }
}


</script>
 
<style>

td {
	padding: 10px;
}

</style>