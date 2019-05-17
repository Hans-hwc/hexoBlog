---
title: Vue使用el-radio-group实现tab选项卡效果
categories: 
- Vue
tags:
- vue
---

效果图
![](https://upload-images.jianshu.io/upload_images/2405826-46bc6a710c61ac14.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

完整源码
```
<template>  
  <div id="app">

    <div style="margin:0 auto;width:325px; margin-bottom:18px">
      <el-radio-group v-model="radio" size="medium">
        <el-radio-button label="代码仓库"></el-radio-button>
        <el-radio-button label="网站"></el-radio-button>
        <el-radio-button label="微博"></el-radio-button>
        <el-radio-button label="公众号" disabled></el-radio-button>
      </el-radio-group>
    </div>
    <!-- tab内容 -->
    <keep-alive>   
      <component v-bind:is="tabView, tabChange(radio)" style="background: #FF0000; width: 100%; height: 100%"></component>  
    </keep-alive>   

  </div>  
</template>  
  
<script>  
  import select1 from './components/xxx1.vue';
  import select2 from './components/xxx2.vue';  
  import select3 from './components/xxx3.vue';  
  import select4 from './components/xxx4.vue';
export default {  
  name: 'app',  
  data () {  
    return {  
      radio: '代码仓库',
      tabView: 'select1',
    }  
  },  
  components: {  
    select1,  
    select2,  
    select3,
    select4
  },  
  methods: {  
    tabChange(tab){
      // this.tabView = tab;  
      console.log("tab："+tab)

      if('代码仓库' == tab){
        this.tabView = 'select1'

      }else if('网站' == tab){
        this.tabView = 'select2'

      }else if('微博' == tab){
        this.tabView = 'select3'
        
      }else if('公众号' == tab){
        this.tabView = 'select4'
        
      }
    }  
  }, 
}  
</script> 
```

小结
1.获取当前点击的是哪个button，通过el-radio-group的v-model="radio"来得到。radio在点击后，值会是label="代码仓库"其中的一个。
2.component通过v-bind动态传值，进而达到切换tab内容的目的。