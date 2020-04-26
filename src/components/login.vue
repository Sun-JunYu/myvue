<template>
  <div>
	<myheader></myheader>

	<section class="featured-block text-center">
		<div class="container">
			<!-- 头部 -->
			<div>

				<Breadcrumb :datas='datas'></Breadcrumb>

			</div>
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
							验证码：
						</td>
						<td>
							<input type="text" v-model='code'>
						</td>
					</tr>

					<tr>
						<td></td>
						<td>
							<img class="imgcode" alt="点击刷新" :src='src'  @click='changecode'>
						</td>
					</tr>
					<tr>
						<td></td>
						<td>
							<!-- 滑块验证码 -->
							<dragVerify 

							:width:"width",
							:height:"height",
							:test:"text"

							></dragVerify>

						</td>
					</tr>
					<tr>
						<td></td>
						<td>
							<Button color='blue' @click='submit'>登录</Button>
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
//导入滑块验证码
import dragVerify from 'vue-drag-verify'

export default {
  data () {
    return {
	  msg: "这是一个变量",

	  // 面包屑导航变量
	  datas:[{title:'首页',route:{name:'index'}},{title:'登录页面'}],

	  // 验证码
	  code :'',
	// 验证码图片地址
	  src:'http://localhost:8000/code/',

	  // 表单数据
	  username :'',
	  password :'',

	  // 声明滑块验证码数据
	  width:320,
	  height:42,
	  text:'请将滑块拖动到右侧'
	
    }
  },

  // 注册组件标签
  components:{
	  'myheader':myheader,
	  'dragVerify':dragVerify
  },

  mounted:function(){

	


	},
  methods:{

	// 刷新验证码
	changecode:function(){

		// 生成随机数
		var num = Math.ceil(Math.random()*10);

		// 进行传参
		this.src = this.src + '?num' + num;

	},

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
		this.axios.get('http://localhost:8000/login/',{params:{
			username:this.username,password:this.password,code:this.code
		}}).then((result)=>{

			console.log(result);

			if (result.data.code==200){

			// 登录成功
			localStorage.setItem('username',result.data.username);
			localStorage.setItem('uid',result.data.uid);

			this.$Message(result.data.message);
			
			//跳转页面
			this.$router.push('/');

			}else{
				this.$Notice(result.data.message)
			}

		});

	}

     
  }
}


</script>
 
<style>

td {
	padding: 10px;
}

.imgcode{
	cursor: pointer;
}

</style>