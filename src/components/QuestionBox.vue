<template>
  <div>
    <b-jumbotron class="my-quiz-container">
      <template v-slot:lead>
        {{ questions }}
      </template>

      <hr class="my-4">

      <p>
        {{ answer }}
        <!-- 正解！ 出し入れしたい -->
      </p>

      <b-button variant="primary" @click="submit('True')" :disabled="isAnswered">Yes</b-button>
      <b-button variant="danger" @click="submit('False')" :disabled="isAnswered">No</b-button><br>
    </b-jumbotron>
    <b-button variant="info" @click="next()" :disabled="!isAnswered">Next</b-button> <!-- 出し入れしたい -->
  </div>
</template>

<script>
export default {
  props: {
    questions: String,
    next: Function,
    submit: Function,
    answer: String,
    isAnswered: Boolean
  }
}
</script>