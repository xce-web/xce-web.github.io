<template>
  <div class="hello">
     <div class="musicStyle">
    <h1>网络红歌榜</h1>
      <h3>单曲/{{total}}首</h3>
        <!-- 视图出所有内容 -->
    <div>
          <li :key="item.id" v-for="item in list" @click="change(item.id)"
               ref="srcMusic" >
             <span id="spa1">{{item.id+"."+item.name+"------"}}</span>
             <span id="spa2">{{item.author}}</span>
   </li>
   </div>    
   <div class="musicStyle-middle">
      <img :class="{active:isActive}" :src="imgSrc">
   </div>
    <div class="musicStyle-main">
     <!-- 动态绑定src地址，自动播放 -->
        <audio   :autoplay="autoplay"
          :src="mp3Src"
            controls></audio>
    </div>
  
  </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
     return{
      isActive:false,
      autoplay:false,
      list:[
      {id:1,name:"无期",image:require("../assets/歌手图片/无期.jpg"),author:"光头华夏",path:require("../assets/MP3文件/1045222350.mp3")},
      {id:2,name:"醉相思",image:require("../assets/歌手图片/醉相思.jpg"),author:"汤茜",path:require("../assets/MP3文件/1401957731.mp3")},
      {id:3,name:"活着",image:require("../assets/歌手图片/活着.jpg"),author:"洪真英",path:require("../assets/MP3文件/2710717364.mp3")},
      {id:4,name:"百花香",image:require("../assets/歌手图片/百花香.jpg"),author:"魏新雨",path:require("../assets/MP3文件/746873269.mp3")},
       {id:5,name:"少年",image:require("../assets/歌手图片/少年.jpg"),author:"梦然",path:require("../assets/MP3文件/4218601620.mp3")},
        {id:6,name:"老人与海",image:require("../assets/歌手图片/老人与海.jpg"),author:"海明威",path:require("../assets/MP3文件/3587648671.mp3")},
          {id:7,name:"像鱼",image:require("../assets/歌手图片/像鱼.jpg"),author:"王贰浪",path:require("../assets/MP3文件/2179691591.mp3")}],
      //给src一个初始值
       mp3Src:require("../assets/MP3文件/1045222350.mp3"),  
       imgSrc:require("../assets/歌手图片/少年.jpg")      
    }
  }
,
  computed:{
    total(){
      return this.list.length
    }
  },
  methods:{
     change(id){
       //获取当前li标签的所有内容
        this.$refs.srcMusic.forEach(
          //value表示li标签的值=this.$refs.srcMusic
           value=>{
             //置空
               value.style.color="";
               value.style.fontSize="";
            })
          //this.refs.srcMusic.[id-1]对应的id的那一个li标签
          //  给所有标签颜色
         
         this.$refs.srcMusic[id-1].style.color="red";
         this.$refs.srcMusic[id-1].style.fontSize="22px";
         //改变src的地址
         this.mp3Src=this.list[id-1].path;
         //改变图片
           this.imgSrc=this.list[id-1].image;
           this.isActive=true;
         //自动播放
           this.autoplay=true;
          } 
       }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .musicStyle{
     margin:0 auto;
     position: relative;
     width:300px;
     height:600px;
     background: aqua;
     display: flex;
     flex-direction: column;
   }
   h1{
     color:blueviolet;
     text-align:center;
   }
   h3{
     color:darkblue
   }
 #span1{
    float: left;
   }
   #span2{
     float: right;
   }
   .musicStyle-main{
     width:300px;
     height:55px;
     position: absolute;
     top:480px;
     left:0px;
    /* box-shadow: 0 0 15px 6px black; */
   }
   .musicStyle-middle{
     position: relative;
   }
   @keyframes imgSrc{
    from {-webkit-transform: rotate(0deg);}
    to {-webkit-transform: rotate(360deg);}

   }
   img{
     height:160px;
     width:160px;
     border-radius: 50%;
     position:absolute;left:0;right:0;margin:0 auto;
     /*图片旋转*/
     
   }
   .active{
      animation: imgSrc 10s linear infinite;
   }
</style>
