<template>
  <div id="app">
    <VueBotUI :messages="data"
              :options="botOptions"
              :bot-typing="botTyping"
              :is-open="true"
              @msg-send="send"/>
  </div>
</template>

<script>
import { VueBotUI } from 'vue-bot-ui';
const axios = require('axios');

export default {
  components: {
    VueBotUI,
  },

  data () {
    return {
      botTyping: false,
      data: [],
      botOptions: {
        botAvatarImg: 'https://image.flaticon.com/icons/png/512/1533/1533105.png',
        botAvatarSize: 64,
        inputPlaceholder: 'Type the message...',
        colorScheme: '#2874A1',
        msgBubbleColorBot: '#fff',
        msgBubbleBgBot: '#6E6897',
        msgBubbleBgUser: '#3aa3b5'
      }
    }
  },

  created: function () {
    let that = this
    this.botTyping = true
    setTimeout(function(){
      that.data.push(that._addMessage('bot', 'Hello. How can I help you?'))
      that.botTyping = false
    }, 2000)
  },

  methods: {
    send: function (data) {
      let that = this;
      this.data.push(this._addMessage('user', data.text));
      this.botTyping = true;

      axios({
        method: 'post',
        url: process.env.VUE_APP_API,
        headers: {},
        data: {
          question: data.text
        }
      }).then( function(response) {
        this.botTyping = true,
        setTimeout(function(){
          that.data.push(that._addMessage('bot', response.answer))
          that.botTyping = false
        }, 2000)
      })
    },

    _addAnswer: function(text) {
      this._addMessage('bot', text)
    },

    _addMessage: function(agent, text) {
      return {
        agent: agent,
        type: 'text',
        text: text
      }
    }
  }

}
</script>

<style>

  * {
    font-family: sans-serif;
  }

  body {
    background-image: url("./assets/background.png");
    background-repeat: no-repeat;
    background-size: cover;
  }

  .qkb-board-content {
    height: 100%;
    overflow: auto;
  }

  .qkb-board-content__bubbles {
    overflow-anchor: auto;
    height: 1px;
  }

</style>
