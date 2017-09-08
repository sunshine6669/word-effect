<template>
  <div id="app">
     <div id="app_warpper" class="styleEditor" ref="styleWarp">
        <!--<pre>{{code}}</pre>-->
        <pre class="" v-html="highlight"></pre>
     </div>
     <div v-html="styleCode">
     
     </div>
  </div>
</template>

<script>
  import Vue from 'vue'
  import PrimisJs from 'prismjs'
  Vue.use(PrimisJs);

export default {
  name: 'app',
  data () {
    return {
      finalCode:`
          /*
          * 大家好，我是webboy 
          */

          /* 首先给所有元素加上过渡效果 */
          * {
            -webkit-transition: all .3s;
            transition: all .3s;
          }
          /* 白色背景太单调了，我们来点背景 */
          html {
            color: rgb(222,222,222); background: rgb(0,43,54); 
          }
          /* 文字离边框太近了 */
          .styleEditor {
            padding: .5em;
            border: 1px solid;
            margin: .5em;
            overflow: auto;
            width: 45vw; height: 90vh;
          }
          /* 代码高亮 */
          .token.selector{ color: rgb(133,153,0); }
          .token.property{ color: rgb(187,137,0); }
          .token.punctuation{ color: yellow; }
          .token.function{ color: rgb(42,161,152); }

          /* 加点 3D 效果呗 */
          html{
            -webkit-perspective: 1000px;
                    perspective: 1000px;
          }
          .styleEditor {
            position: fixed; left: 0; top: 0; 
            -webkit-transition: none; 
            transition: none;
            -webkit-transform: rotateY(10deg) translateZ(-100px) ;
                    transform: rotateY(10deg) translateZ(-100px) ;
          }

          /* 接下来我给自己准备一个编辑器 */
          .resumeEditor{
            position: fixed; right: 0; top: 0;
            padding: .5em;  margin: .5em;
            width: 48vw; height: 90vh; 
            border: 1px solid;
            background: white; color: #222;
            overflow: auto;
          }
          /* 好了，我开始写简历了 */



          /* 这个简历好像差点什么
          * 对了，这是 Markdown 格式的，我需要变成对 HR 更友好的格式
          * 简单，用开源工具翻译成 HTML 就行了
          */

          /* 再对 HTML 加点样式 */
          .resumeEditor{
            padding: 2em;
          }
          .resumeEditor h2{
            display: inline-block;
            border-bottom: 1px solid;
            margin: 1em 0 .5em;
          }
          .resumeEditor ul,.resumeEditor ol{
            list-style: none;
          }
          .resumeEditor ul> li::before{
            content: '•';
            margin-right: .5em;
          }
          .resumeEditor ol {
            counter-reset: section;
          }
          .resumeEditor ol li::before {
            counter-increment: section;            
            content: counters(section, ".") " ";  
            margin-right: .5em;
          }
          .resumeEditor blockquote {
            margin: 1em;
            padding: .5em;
            background: #ddd;
          }
          http://strml.net/
      `,
      code:``
    }
  },
  computed:{
     styleCode(){
       return "<style>"+this.code+"</style>"
     },
     highlight(){
       return Prism.highlight(this.code, Prism.languages.css)
     }
  },
  methods:{
    /*async makeResume(){
       await this.printCon();
       console.log("写完了....");
    },*/
     makeResume(){
      this.printCon();
       console.log("写完了....");
    },
     printCon(){
      // return new Promise((resolve,reject)=>{
          var n = 0;
          var timer = setInterval(()=>{
             // app_warpper.innerHTML += this.showCon.slice(n,n+1);
              this.code = this.finalCode.substring(0,n);
              this.$nextTick(() => {
                 this.$refs.styleWarp.scrollTop = 1000
              })
              if(n>this.finalCode.length-1){
                clearInterval(timer);
                console.log("清楚动画.......");
              }else{
                n+=1;
              }
          },10);
     }
  },
  created(){
        this.makeResume();
  }
}
</script>
<style>
</style>
