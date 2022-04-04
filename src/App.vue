<template><!-- 表示する内容 -->
  <div id="app">
    <input type="radio" v-model="playerHand" id="g" value="0"><label for="g">グー</label>
    <input type="radio" v-model="playerHand" id="c" value="1"><label for="c">チョキ</label>
    <input type="radio" v-model="playerHand" id="p" value="2"><label for="p">パー</label>
    <p>あなたは{{ hands[playerHand] }}を出そうとしています</p>
    <p><button @click="janken()">ボタン</button></p>
    <p>{{ message }}</p>
    <ul>
      <!-- ここのhandは変数 -->
      <li v-for="(hand, index) in historyData" :key= "index">
        <!-- indexである必要性はないが、かぶるといけないので、とりあえずindex -->
        {{ hands[hand.playerHand]}} {{ hands[hand.computerHand] }} {{ hand.judge }}
      </li>
    </ul>
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
      computerHand: 0,
      historyData: [
        { playerHand: '', computerHand: '', judgeMessage: '' }
      ],
      judgeMessage: '',
      judge: ['あいこです', 'コンピュータの勝ちです', 'あなたの勝ちです'],
  }
},
  methods: {
    janken() {

      // let judgeMessage = ''
      this.computerHand = Math.floor(Math.random() * 3)
      const result = (this.playerHand - this.computerHand + 3) % 3
      this.message = 'コンピュータは' + this.hands[this.computerHand] + 'を出しました。'
      if(result == 0) {
        this.message += this.judge[0]
        this.judgeMessage = this.judge[0]
      } else if(result == 1) {
        this.message += this.judge[1]
        this.judgeMessage = this.judge[1]
      } else if(result == 2) {
        this.message += this.judge[2]
        this.judgeMessage = this.judge[2]
      }
      // push内のjudgeは名前、この名前をもとに、v-for内で結果を呼び出している
      this.historyData.push({ playerHand: this.playerHand, computerHand: this.computerHand, judge: this.judgeMessage })
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
