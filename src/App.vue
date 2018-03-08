<template>
  <div id="app">
    <div class="computed">
      {{reverse}}
    </div>
    <div class="change" @click="change">
      {{msg.name}}
    </div>
    <div class="change_name">
      {{change_name}}
    </div>

  </div>
</template>

<script>
  import fastclick from 'fastclick'
  import WechatShare from 'johnny-wechat-share'

//import files
  const requireContext = require.context("./assets/img", true, /^\.\/.*\.png$/);
  const images = requireContext.keys().map(requireContext);
  console.log(images);


  //wechat share

  let option={}
  option.api='http://h5.2smart.cn/wechat/js/'
  option.shareData={
    appmessage: {
      title: "",//好友分享标题
      desc: "",//好友分享描述
      img_url: "",//好友分享图片
      link: "" //好友分享链接
    },
    timeline: {
      title: "",//朋友圈分享标题
      img_url: "",//朋友圈分享图片
      link: ""//朋友圈分享链接
    }
  };

  window.WECHAT_SHARE = new WechatShare(option);

  let msg=[];
  msg.push({name:"zhangsan"})
  msg.push({name:"lisi"})
  msg.push({name:"wangwu"})
  msg.push({name:"zhaoliu"})
  msg.push({name:"guoqi"})
  msg.push({name:"sunba"})
  msg.push({name:"gai"})

  let num=0;let now=0;
  export default {
  name: 'app',
  data () {
    return {
      message:"hello",msg:msg[0],names:msg,
    }
  },
    methods:{
        change:function(){
          num++;
          this.msg=msg[num];
          if(num==this.names.length-1){
            num=0;
          }
          //return num;
        }
    },
  computed:{
      reverse:function(){
        return this.message.split('').reverse().join(" ")
      },
    change_name:function(){
      this.msg.name
      return num;
    }

  },
  mounted: function () {
    fastclick.attach(this.$el)
  }
}
</script>

<style>
@import "assets/css/base.css";
@import "assets/css/mobile_h5.css";
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width:100%;height:100%;
}
  .computed{
    width: 100%;height:300px;background: #ccc;
    line-height: 300px;
  }
  .change{
    width: 100%;height:300px;background: #f0f0f0;
    line-height: 300px;
  }
  .change_name{
    width: 100%;height:300px;background: gray;
    line-height: 300px;
  }
</style>
