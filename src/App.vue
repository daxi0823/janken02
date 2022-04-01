<template><!-- 表示する内容 -->
  <div id="app">
    <input type="radio" v-model="playerHand" id="g" value="0"><label for="g">グー</label>
    <input type="radio" v-model="playerHand" id="c" value="1"><label for="c">チョキ</label>
    <input type="radio" v-model="playerHand" id="p" value="2"><label for="p">パー</label>
    <p>あなたは{{ hands[playerHand] }}を出そうとしています</p>
    <p><button @click="janken()">ボタン</button></p>
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      message: '',
      hands: ['グー', 'チョキ', 'パー'],
      playerHand: 0,
      computerHand: 0
  }
},
  methods: {
    janken() {
      this.computerHand = Math.floor(Math.random() * 3)
      const result = (this.playerHand - this.computerHand + 3) % 3
      this.message = 'コンピュータは' + this.hands[this.computerHand] + 'を出しました。'
      if(result == 0) {
        this.message += 'あいこです' 
      } else if(result == 1) {
        this.message += 'コンピュータの勝ちです'
      } else if(result == 2) {
        this.message += 'あなたの勝ちです'
      }
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
</style>
