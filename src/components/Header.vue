<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled><b>My Quiz</b></b-nav-item>
      <b-nav-item disabled>{{ correctCount }}/{{ totalCount }}</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
  props: {
    correctCount: Number,
    totalCount: Number
  }
}
</script>