<template>
    <div class="info-mingzi">
        <!--顶部 -->
        <mt-header title="修改昵称" fixed>
          <router-link to="/info" slot="left">
            <mt-button icon="back"></mt-button>
          </router-link>
          <mt-button id="btn-save" slot="right" @click="updateNick" :disabled="disable">保存</mt-button>
        </mt-header>
        <!-- 修改 -->
        <div id="mingzi">
            <mt-field label="新昵称" placeholder="输入新昵称" type="text" v-model="nickName"></mt-field>
        </div>
    </div>
</template>
<script>
import {mapState} from 'vuex'
export default{
   data(){
       return {
           nickName:"",
           disable:true
       }
   },
   computed:{
       ...mapState(["userInfo"])
   },
   methods:{
       updateNick(){
           let uid=this.$store.state.userInfo.uid
        //console.log(this.state.userInfo.uid)
        this.axios.post(`/update?uid=${uid}`,`nickname=${this.nickName}`).then((res)=>{
            console.log(res)
            if(res.data.code==200){
                let ss=window.sessionStorage;
                // console.log(JSON.parse(sessionStorage.getItem('userInfo')).nickname)
                let userInfo=JSON.parse(sessionStorage.getItem('userInfo'))
                userInfo.nickname=this.nickName
                // console.log(userInfo)          
                ss.setItem('userInfo',JSON.stringify(userInfo))
                this.$store.commit('setInfo',userInfo)
                // console.log(this.$store.state.userInfo)
                this.$toast({
                    message:"修改成功",
                    position:"bottom",
                    duration:500
                })
                this.$router.push('/info')
            }else{
                 this.$toast({
                    message:"系统忙,请稍后再试",
                    position:"bottom",
                    duration:500
                })
            }
        })
       }
   },
   watch:{
       nickName:function(val){
           if(val!=''){
               this.disable=false
           }else{
               this.disable=true
           }
       }
   }
}
</script>
<style>
.info-mingzi .mint-header{
        background-color: #86998c;
        height: 50px;
}
.info-mingzi #btn-save{
    background-color: #66b081;
    width: 65px;
    height: 35px;
}
.info-mingzi #mingzi{
    margin-top: 50px;
}
.info-mingzi .mint-cell:last-child {
    background-image: linear-gradient(0deg,#d9d9d9,#d9d9d9 100%,transparent 0);
    margin-left: 10px;
}
</style>

