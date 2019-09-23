<template>
  <div id="app">
    <Header />

    <b-container class="bv-example-row">
      <b-row>
        <b-col md="6" offset-md="3">
          <!-- QuenstionBox（データを渡したいコンポーネント）の中にv-bindで渡したいデータを定義する。 -->
          <QuestionBox
            v-if="questions != null"
            v-bind:questions="questions[index].question"
            v-bind:next="next"
            v-bind:submit="submit"
            v-bind:answer="answer"
            v-bind:isAnswered="isAnswered"
          /></b-col>
      </b-row>
    </b-container>
    <!-- nullのまま表示するなって指示 -->
    <p
    v-if="questions != null"
    >
    <!-- {{ index }}<br> デバッグ用 -->
    <!-- {{ correctAnswer }}
    {{ questions }} -->
    </p>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'app',
  components: {
    Header,
    QuestionBox
  },
  data() {
    return { //dataファンクションに返り値を入れる(jsonオブジェクトにする必要がある)
      questions: null, //変数の初期値を入れなきゃいけなくてnullは型を気にしなくていい形式（0で初期化するのと同じ。nullはintでも文字列でもない）
      index: 0,
      answer: '',
      isAnswered: false
    }
  },
  mounted() {
    fetch('https://opentdb.com/api.php?amount=10&category=11&difficulty=easy&type=boolean', {
      method: 'get' //getでapiを叩いてる
    })
      .then((response) => {
        return response.json() //apiのレスポンスをresponseと言う名前で受けとってjson形式に変換してる
      })
      .then((jsonData) => {
        this.questions = jsonData.results //上でリターンしたjsonオブジェクトのresultsキーのバリューをデータメソッドで定義したquestionsに代入してる
      })
  },
  methods: {
    next() { //index（配列の何番目を表示したい）のデータは App.vueが持ってるからここで書く。
      this.index++ //++で順番を増やすnext関数を作ってる
      this.answer = ''
      this.isAnswered = false
    },
    submit(selectedAnswer) {
      this.answer = this.correctAnswer === selectedAnswer ? '正解！' : '不正解！'
      this.isAnswered = true
    }
  },
  computed: {
    correctAnswer() {
      return this.questions[this.index].correct_answer
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
