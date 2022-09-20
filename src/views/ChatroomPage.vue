<template>
  <div class="container">
    <Navbar />
    <ChatWindow :messages="messages" />
  </div>
</template>

<script>
import Navbar from '../components/NavBar'
import ChatWindow from '../components/ChatWindow'
import axios from 'axios'
export default {
  // ======= 👇 ここから変更する =======
  components: { Navbar, ChatWindow },
  data () {
    return {
      messages: [],
    }
  },
  methods: {
    async getMessages () {
      try {
        const res = await axios.get('http://localhost:3000/messages', {
          headers: {
            uid: window.localStorage.getItem('uid'),
            "access-token": window.localStorage.getItem('access-token'),
            client:window.localStorage.getItem('client')
          }
        })
        if (!res) {
          new Error('メッセージ一覧を取得できませんでした')
        }
        this.messages = res.data
      } catch (err) {
        console.log(err)
      }
    },
  },
  mounted() {
    this.getMessages()
  },
}
</script>

<style scoped>
</style>