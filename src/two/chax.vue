<template>
  <div class='chax'>
     <div class='out'>
       <form>
         <fieldset class='info'>
           <legend>会员基本信息</legend>
           <div class='box'>
             <div >
               <p class='bon'>
                姓名：
                <input type="text"  v-model='xm_'>
              </p>
              <p class='hs'>
                邮箱：
                <input type="text" v-model='yx'>
              </p>
             </div>
            <div >
              <p class='bon'>
             手机号：
             <input type="text"  v-model='phone'>
             </p>
           <p>
             证件号：
             <input type="text"  v-model='sfz'>
           </p>
            </div>
            <div>
              <a @click.prevent='btn' class='sp'>查询</a>
            </div>
           </div>
         </fieldset>
         <fieldset class='info'>
           <legend>账户信息</legend>
           <div class='box'>
             <div>
             <p class='hs'>
             积分
             <input type="text" name="jf" v-model='jf'>
           </p>
           </div>
           <div>
             <p class='hs'>
             平驾币：
             <input type="text" name="pjb" v-model='pjb'>
           </p>
           </div>
           <div>
             <router-link to='/huiy/chongz'>

               <a class='sp'>充值</a>
             </router-link>
              
            </div>
           </div>
         </fieldset>
         <fieldset class='info'>
           <legend class='xf'>消费记录</legend>
           <ul>
             <li>
               <span>时间</span>
               <span>车型</span>
               <span>租凭方式</span>
               <span>处理状态</span>
               <span>操作</span>
             </li>
             <li class='hov' v-for='(item,index) in lists' :key='index'>
               <span>{{item.returntime}}</span>
               <span>{{item.quality}}</span>
               <span>{{item.rentStyle}}</span>
               <span>{{item.orderStatue}}</span>
               <span>{{item.operation}}</span>
             </li>
           </ul>
         </fieldset>
       </form>
     </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
        xm_:'',
        phone:'',
        sfz:'',
        jf:'',
        pjb:'',
        yx:'',
       list:'',
       lists:'',
        operation: "",
      orderStatue: "",
      quality: "",
      rentStyle: "",
      returntime: ""
    }
  },
  methods: {
      btn(){
        this.$axios.post(
      'http://wlz.in.8866.org:30167/edit/findByPhone',
       this.$qs.stringify(
       {
          "mname":this.xm,
          "phone":this.phone
       })).then((res)=>{
         this.list=res.data;
       this.yx=this.list[0].email;
       this.sfz=this.list[0].identity;
       this.xm_=this.list[0].username;
       this.jf=this.list[0].integral;
       this.pjb=this.list[0].pjmoney;
      this.lists=this.list[1]
     
       }).catch((err)=>{
         console.log(err)
       });
    

      }
  }
}
</script>

<style scoped lang='less'>
.chax{
    margin:30px 0;
    padding:0 30px;
    background:#fff;
    border-radius:10px;
      legend{
        padding-top:20px;
      }
      .box{
      display:flex;
      justify-content:space-between;
       .bon{
           margin-bottom:20px;
       }
       .sp{
         display:inline-block;
         width:60px;
        height:30px;
        line-height:30px;
        text-align:center;
        background:#ffe009;
        border-radius:5px;
       }
      p{
        height:40px;
        input{
          border:1px solid #00a0e9;
          border-radius:5px;
          width:248px;
          height:38px;
          padding-left:20px;
        }
      }
      .hs{
        input{
          border:1px solid #ccc;
        }
      }
    }
    ul{
      margin:0 -45px;
      padding-bottom:30px;
      li{
        border-top: 1px solid #ccc;
        border-bottom: 1px solid #ccc;
        display:flex;
        justify-content:space-between;
        height:60px;
        line-height:60px;
        span{
          display:block;
          width:150px;
          text-align:center;
        }
        span:nth-child(1){
          padding-left:30px;
        }
      }
      .hov:hover{
         background:rgb(235, 235, 235);
      }
    }
    
    
}

@media all and (max-width:1366px){
  .chax{
    margin:21px 0;
    padding:0 21px;
    background:#fff;
    border-radius:7px;
      legend{
        padding-top:14px;
      }
      .box{
      display:flex;
      justify-content:space-between;
       .bon{
           margin-bottom:14px;
       }
       .sp{
         display:inline-block;
         width:42px;
        height:21px;
        line-height:21px;
        text-align:center;
        background:#ffe009;
        border-radius:3px;
       }
      p{
        height:28px;
        input{
          border:1px solid #00a0e9;
          border-radius:3px;
          width:173px;
          height:26px;
          padding-left:14px;
        }
      }
      
      .hs{
        input{
          border:1px solid #ccc;
        }
      }
    }
    
    ul{
      margin:0 -32px;
       padding-bottom:21px;
      li{
        border-top: 1px solid #ccc;
        border-bottom: 1px solid #ccc;
        display:flex;
        justify-content:space-between;
        height:42px;
        line-height:42px;
        span{
          display:block;
          width:105px;
          text-align:center;
        }
        span:nth-child(1){
          padding-left:21px;
        }
      }
      .hov:hover{
         background:rgb(235, 235, 235);
      }
    }
   
}
}
</style>
