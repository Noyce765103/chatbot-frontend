<template>
  <div id="app" class='myframe'>
    <el-row >
      <el-col :span="12"><div class="grid-content bg-purple">
        <el-container>
  <el-header>Header</el-header>
  <el-main>Main</el-main>
  <el-footer>Footer <input v-model='question' type="text"> <button @click="send_question">发送</button></el-footer>
</el-container>
        </div></el-col>
      <el-col :span="12"><div class="grid-content bg-purple-light">
        大锅饭苟富贵
        </div></el-col>
    </el-row>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data () {
    return {
      question:'高血压可以吃什么药'
    }
  },
  methods: {
    send_question:function(e){
      this.$axios({
        url:'http://127.0.0.1:5000/chat',
        method:'post',
        data:{'question':this.question}
      }).then((res)=>{
        console.log(res.data)
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.myframe {
  height: 100%;
  width: 100%;
  background-color:yellowgreen;
}
</style>
