<template>
  <div>
     <mt-tabbar v-model="selected" fixed>
      <mt-tab-item id="home">
        <img v-if="selected == 'home'"  slot="icon"  src="image/home/icon/nav-icon-jiaoshixinxi_active.svg"  alt="" />
        <img  v-else  slot="icon"  src="image/home/icon/nav-icon-jiaoshixinxi.svg"  alt="" />
        首页
      </mt-tab-item>
      <mt-tab-item id="article">
        <img  v-if="selected == 'article'"  slot="icon" src="image/home/icon/nav-icon-gonggao_active.svg"  alt="" />
        <img  v-else  slot="icon"  src="image/home/icon/nav-icon-gonggao.svg"  alt="" />
        列表
      </mt-tab-item>
      <mt-tab-item id="recommend">
        <img  v-if="selected == 'recommend'"  slot="icon"  src="image/home/icon/nav-icon-baseinfo_active.svg"  alt=""  />
        <img
          v-else
          slot="icon"
          src="image/home/icon/nav-icon-baseinfo.svg"
          alt=""
        />
        推荐
      </mt-tab-item>
      <mt-tab-item id="mine">
        <img
          v-if="selected == 'mine'"
          slot="icon"
          src="image/home/icon/nav-icon-gerenxiaoxi_active.svg"
          alt=""
        />
        <img
          v-else
          slot="icon"
          src="image/home/icon/nav-icon-gerenxiaoxi.svg"
          alt=""
        />
        我的
      </mt-tab-item>
    </mt-tabbar>
  </div>
</template>
<script>
export default {
  data(){
    return {
      selected:this.select
    }
  },
   props: {
    select: {
        type: String, 

         }
      },
  watch: {
    // 监听器，监听变量的更新
    selected(newvalue) {
      // newvalue 是selected的新值
      if (newvalue == "home") {
        this.$router.push("/");
      } else if (newvalue == "article") {
        this.$router.push("/article");
      } else if (newvalue == "recommend") {
        this.$router.push("/recommend");
      } else if (newvalue == "mine") {
        this.$router.push("/mine");
      }
    }
  },
  mounted(){
    // console.log(this.selected)
  }
}
</script>