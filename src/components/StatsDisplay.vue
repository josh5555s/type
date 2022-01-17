<template>
  <div>
    <p>Total time: {{ totalTime }}</p>
    <p>Total average: {{ totalTime }}</p>
  </div>
</template>

<script>
export default {
  props: [],
  data: () => ({
    totalTime: 0,
    totalCorrect: 0,
    totalIncorrect: 0,
    totalAverage: 0,
    wordsPerMinute: 0, // for last 25 inputs, 5 correct char == word, incorrect == - char
    highestWordsPerMinute: 0,
  }),
  methods: {},
};
</script>

<style lang="scss" scoped>
div {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}
</style>
