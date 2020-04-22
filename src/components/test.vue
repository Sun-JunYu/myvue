<template>
    <div>
        <!-- 购物车 -->
        <table>

            <tr> <td>名称</td> <td>数量</td> <td>价格</td> </tr>

            <tr v-for="(item,index) in tlist">

                <td>

                    {{ item.test }}

                </td>

                <td>
                    <button @click="minus(index,1)">-</button>
                    <input type="text" v-model='item.num'>
                    <button @click="minus(index,0)">+</button>

                </td>

                <td>

                    {{ item.prict }}

                </td>


            </tr>

        </table>
        总数量：{{ totalCount()[0] }} <br/>
        总价格：{{ totalCount()[1] }}<br/><br/>
        
        {{ counter }}
        <button @click='counter++'>加一</button> <br><br><br>

        {{ reverse_msg2() }}    <br>

        {{ reverse_msg }}
        <br><br><br>

        <ul>

            <li v-for="(item,index) in tlist" :class="{
                on:index%2==0,off:index%2!=0
            }">

                {{ item.test }}

            </li>

        </ul>

        <div v-if="type === '狗'">狗</div>

        <div v-else-if="type === '猫'">B</div>

        <div v-else>
            既不是狗，也不是猫。
        </div>

        <h2 v-if='ok'>今天天气不错</h2>

        <h2 v-show='ok'>阳光明媚</h2>

        <div v-html='msg'></div>
        {{ msg }}    


    </div>
</template>


<script>
    export default{
        data(){

            return{
                
                msg:'<h1>这是一个变量</h1>',
                ok:1,
                type:'狗',
                tlist:[{test:'电脑',num:3,prict:9000},{test:'鼠标',num:3,prict:100},{test:'键盘',num:3,prict:200},{test:'耳机',num:3,prict:90}],
                counter:0,

            }  
            
            
        },

        // 监听属性
        watch:{

            counter:function(nval,oval){

                console.log('计数器由'+oval+'变换为新的'+nval);

            }

        },

        // 计算属性
        computed:{

            // 反转
            reverse_msg:function(){
                console.log(this.msg.split(''));

                return this.msg.split('').reverse().join('');

            }

        },



        // 钩子方法
        mounted:function(){


        },

        // 自定义方法
        methods:{

            // 购物车总汇
            totalCount:function(){

                // 默认数量
                let total = 0;
                let prict = 0;

                //遍历
                for (let i=0,l=this.tlist.length;i<l;i++){

                    // 汇总
                    total += this.tlist[i].num;
                    prict += this.tlist[i].prict;

                }

                return [total,prict]

            },

            

            // // 购物车减法
            // minus:function(index){

            //     if (this.tlist[index].num > 0){

            //         this.tlist[index].num--;

            //     }
                    

            // },

            // // 购物车加法
            // add:function(index){

            //         this.tlist[index].num++;
                    
            // },
            minus:function(index,on){

                if (on){
                    if (this.tlist[index].num>0){
                        this.tlist[index].num--;
                    }
                    
                }
                else{
                    this.tlist[index].num++;
                }

            },


            // 自定义计算属性
            reverse_msg2:function(){

                console.log(this.msg.split(''));

                return this.msg.split('').reverse().join('');

            },


        },

    }

</script>


<style>

/* .on {background-color: aquamarine;}
.off {background-color: chartreuse;} */

</style>