<template>
  <div id="app">
    <p>現在 {{ jadgeCount[2] }}勝 {{ jadgeCount[1] }}敗 {{ jadgeCount[0] }}分 (勝率{{ Math.round(jadgeCount[2] / historyData.length * 100) }}%) です。</p>
    <input type="radio" v-model="playerHand" id="g" value="0"><label for="g">グー</label>
    <input type="radio" v-model="playerHand" id="c" value="1"><label for="c">チョキ</label>
    <input type="radio" v-model="playerHand" id="p" value="2"><label for="p">パー</label>
    <p>あなたは{{ hands[playerHand] }}を出そうとしています。</p>
    <p><button @click="janken()">ジャンケン</button></p>
    <p>{{ message }}</p>
    <ul>
      <li>
        <span>あなた</span><span>コンピュータ</span><span>勝敗</span>
      </li>
      <li v-for="(hand, index) in historyData" :key="index"><span>{{ hands[hand.playerHand] }}</span><span>{{ hands[hand.computerHand] }}</span><span>{{ hand.jadge }}</span></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      message: '',
      hands: ['✊グー', '✌️チョキ', '✋パー'],
      playerHand: 0,
      computerHand: 0,
      historyData: [],
      jadgeCount: [0, 0, 0]
    }
  },
  methods: {
    janken() {
      let jadge = ''
      this.computerHand = Math.floor(Math.random() * 3)
      const result = (this.playerHand - this.computerHand + 3) % 3
      this.message = 'コンピュータは' + this.hands[this.computerHand] + 'を出しました、'
      if(result == 0) {
        this.message += 'あいこです'
        jadge = '💁あいこ'
      } else if(result == 1) {
        this.message += 'コンピュータの勝ちです'
        jadge = '🙅負け'
      } else if(result == 2) {
        this.message += 'あなたの勝ちです'
        jadge = '🙆勝ち'
      }
      this.historyData.push({ playerHand: this.playerHand, computerHand: this.computerHand, jadge: jadge })
      if(jadge == '💁あいこ') {
        this.jadgeCount[0]++
      } else if(jadge == '🙅負け') {
        this.jadgeCount[1]++
      } else if(jadge == '🙆勝ち') {
        this.jadgeCount[2]++
      }
    }
  },
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

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  width: 50vw;
  margin: 0 auto;
}
li {
  border-bottom: 1px solid #ccc;
}
span {
  display: inline-block;
  width: 10rem;
  line-height: 3rem;
  text-align: center;
  font-size: .8rem;
}
</style>
