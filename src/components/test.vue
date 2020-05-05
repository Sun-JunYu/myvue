<template>
	<div>

		<!--购物车-->

		<table>

			<tr> <td>名称</td> <td>数量</td> <td>价格</td> </tr>
			
			<tr v-for="(item,index) in tlist">
				
				<td>
						
						{{ item.text }}

				</td>

				<td>

						<button @click="minus(index,'-')">-</button>

						<input type="number" v-model="item.num" >

						<button  @click="minus(index,'+')" >+</button>

				</td>

				<td>
						
						{{ item.price }}

				</td>


			</tr>



		</table>

		总数量:{{ totalCount(0) }}

		&nbsp;&nbsp;

		总价格:{{ totalCount(1) }}



		<br /><br />

		{{ counter }}
		<button @click="counter++" >点我就加一</button>

		{{ reverse_msg2() }}

		{{ reverse_msg }}

		<ul>
			
			<li v-for="(item,index) in tlist" :class="{on:index%2==0,off:index%2!=0}" >
				
				{{ item.text }}

			</li>


		</ul>


		<div v-if="type === 'A'">A</div>

		<div v-else-if="type === 'B'">B</div>

		<div v-else>
			
			既不是A也不是B

		</div>



		<h2 v-if="ok">Hello World</h2>

		<h2 v-show="ok">Hello World</h2>
		
		<div v-html="msg"></div>

		{{ msg }}


	</div>
</template>


<script>
	
	export default{
		//定义数据
		data(){

			return {

				msg:'<h1>这是一个变量</h1>',
				ok:0,
				type:'B',
				tlist:[{text:'汽车',num:1,price:10},{text:'化妆品',num:1,price:8},{text:'衣服',num:1,price:1},{text:'牛奶',num:1,price:5}],
				counter:0

			}


		},
		//监听属性
		watch:{

			counter:function(nval,oval){


				console.log('计数器由'+oval+'变换为新的'+nval);

			}

		},
		//计算属性
		computed:{

			//反转
			reverse_msg:function(){

				console.log(this.msg.split(''));

				return this.msg.split('').reverse().join('');

			}

		},
		//钩子方法  created
		mounted:function(){



		},
		//自定义方法
		methods:{

			//汇总数量
			totalCount:function(type){

				//默认数量
				let total = 0;

				//默认价格
				let totalprice = 0;

				//遍历
				for(let i=0,l=this.tlist.length;i<l;i++){


					//总数量累加
					total += parseInt(this.tlist[i].num);

					//总价格相加
					totalprice += (this.tlist[i].num * this.tlist[i].price);


				}

				if(type==0){

				return total;

			}else{
				return totalprice;
			}

			},
			//购物车减法
			minus:function(index,type){


				if(type=="-"){

				if(this.tlist[index].num > 0){

				this.tlist[index].num--;

				}

			}else{

				this.tlist[index].num++;
			}

			},
			//购物车加法
			add:function(index){

		
				this.tlist[index].num++;

			},
			//自定义计算属性
			reverse_msg2:function(){

				console.log(this.msg.split(''));

				return this.msg.split('').reverse().join('');

			}



		}

	}

</script>


<style>

.on {
	background:rebeccapurple;
	color:white;
}
.off {
	background:red;
	color:black;

}

</style>