<template>
  <div id="app">
    <VueBotUI :messages="data" :options="botOptions" :bot-typing="botTyping" :is-open="true"/>
  </div>
</template>

<script>
import { VueBotUI } from 'vue-bot-ui'

export default {
  components: {
    VueBotUI,
  },

  data () {
    return {
      botTyping: false,
      data: [
        {
          agent: 'bot',
          type: 'text',
          text: 'Hello. How can I help you?'
        },
        {
          agent: 'user',
          type: 'text',
          text: 'I need a new laptop',
        },
      ],
      botOptions: {
        botAvatarImg: 'https://image.flaticon.com/icons/png/512/1533/1533105.png',
        botAvatarSize: 64,
        inputPlaceholder: 'Type the message...'
      }
    }
  }
}

</script>

<style>
  * {
    font-family: sans-serif;
  }
</style>
