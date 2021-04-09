<template>
  <div id="app">
    <div class="main-container">
      <div class="chat-container">
        <p class="chat-header">聊天机器人</p>
        <div class="chat-message-container">
          <div v-for="(message, index) in messageList" :key="message">
            <div :class="`message-box ${index % 2 === 0 ? 'left-message-box' : ''}`">
              <span :class="`${index % 2 === 0 ? 'right-message-text' : 'left-message-text'}`">{{ message }}</span>
            </div>
          </div>
        </div>
        <div class="chat-input-container">
          <el-input
            class="chat-input"
            type="textarea"
            autosize
            row="2"
            placeholder="请输入问题"
            resize="none"
            v-model="question"
          />
          <el-button
            type="primary"
            size="medium"
            class="send-button"
            @click="sendQuestion"
            >发送</el-button
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { Input, Button } from "element-ui";

export default {
  name: "App",
  components: {
    HelloWorld,
    Button,
    Input,
  },
  data() {
    return {
      // question: "高血压可以吃什么药",
      question: "",
      messageList: [],
    };
  },
  methods: {
    /** send_question */
    /** 驼峰式命名法 你懂？ */
    /** 在类中函数可以直接这样写 */
    sendQuestion() {
      const param = {
        question: this.question
      }
      /** 点击后先将自己的问题消息推入数组 */
      this.messageList.push(this.question)
      /** 清空v-model绑定的input值 */
      this.question = ''
      /** 发送请求 */
      console.log(param)
      /** axios的baseURL可以在main中配置好，发请求如下 */
      this.$axios
        .post("chat", param)
        .then((res) => {
          console.log(res, "result");
          /** 向数组中push message数据 */
          // this.messageList.push(res.message)
        })
        .catch((err) => {
          console.log(err, "err");
        });
    },
  },
};
</script>

<style scoped>
.main-container {
  width: 800px;
  height: 100%;
  margin: auto;
  background-color: #edf2f9;
  border-radius: 12px;
}

.chat-container {
  width: 400px;
  height: 100%;
  background-color: #edf2f9;
  border: 1px solid blue;
  border-radius: 12px;
}

.chat-header {
  height: 60px;
  display: flex;
  align-items: center;
  padding-left: 16px;
  margin: 0;
  border-bottom: 1px solid #dde0e9;
  font-size: 18px;
  font-family: SegoeUI-Semibold, SegoeUI;
  font-weight: 600;
  color: #040405;
  box-sizing: border-box;
}

.chat-message-container {
  width: 100%;
  height: 705px;
  padding-top: 20px;
  border-bottom: 1px solid #dde0e9;
  background-color: #edf2f9;
  overflow: hidden;
  box-sizing: border-box;
}

.chat-input-container {
  display: flex;
  align-items: center;
  width: 400px;
  height: 65px;
  padding: 16px;
  box-sizing: border-box;
}

.chat-input {
  width: 300px;
  /* height: 158px; */
}

.send-button {
  display: flex;
  align-items: center;
  height: 33px;
  margin-left: 5px;
}

.message-box {
  display: flex;
  align-items: center;
  margin-left: 5px;
  margin-right: 5px;
}

.left-message-box {
  justify-content: flex-end;
}

.left-message-text {
  display: inline-block;
  background: #ffffff;
  padding: 8px 16px;
  box-shadow: 0px 1px 5px 0px #b7d0dc;
  border-radius: 12px 12px 12px 0px;
  margin-bottom: 16px;
  font-size: 12px;
  max-width: 160px;
  word-wrap: break-word;
  white-space: pre-wrap;
}

.right-message-text {
  display: inline-block;
  background: #c5e4ff;
  padding: 8px 16px;
  box-shadow: 0px 1px 5px 0px #b7d0dc;
  border-radius: 12px 12px 0px 12px;
  margin-left: 5px;
  margin-bottom: 16px;
  font-size: 12px;
  max-width: 160px;
  word-wrap: break-word;
  white-space: pre-wrap;
}
</style>
