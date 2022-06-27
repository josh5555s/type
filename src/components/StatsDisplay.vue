<template>
  <div>
    <p>Correct: {{ setCorrect }}</p>
    <p>Errors: {{ setErrors }}</p>
    <p>Accuracy: {{ setAccuracy }}</p>
    <!-- <p>CPS: {{ charPerSecond }}</p>
    <p>High CPS: {{ currentSetHighCPS }}</p> -->
    <p>Current WPM: {{ wordsPerMinute }}</p>
    <p>Highest WPM: {{ currentSetLocalHighWPM }}</p>
  </div>
</template>

<script>
export default {
  props: ['charArchive', 'currentSet', 'charGroups'],
  data: () => ({
    currentHighCPS: [0, 0, 0, 0, 0, 0, 0],
    currentHighWPM: [0, 0, 0, 0, 0, 0, 0],
    currentSetLocalHighWPM: '',
  }),
  computed: {
    setName() {
      return this.charGroups[this.currentSet];
    },
    currentSetArchive() {
      return this.charArchive.filter((item) => item.charSet == this.currentSet);
    },
    setCorrect() {
      return this.currentSetArchive.length;
    },
    setErrors() {
      let errors = 0;
      this.currentSetArchive.forEach((item) => {
        errors += item.errorCount;
      });
      return errors;
    },
    setAccuracy() {
      let sa = 'tbd';
      if (this.setCorrect > 0) {
        sa = `${Math.round((1 - this.setErrors / this.setCorrect) * 100)}%`;
      }
      return sa;
    },
    charPerSecond() {
      let cps = 'tbd';
      if (this.setCorrect > 10) {
        const lastTen = this.currentSetArchive.slice(-10);
        let lastTenTime = 0;
        lastTen.forEach((item) => {
          if (item.time < 10000) {
            lastTenTime += item.time;
          }
        });
        const millisecondsPerChar = lastTenTime / 10;
        const secondsPerChar = millisecondsPerChar / 1000;
        cps = Math.round((1 / secondsPerChar) * 100) / 100;
      }
      return cps;
    },
    wordsPerMinute() {
      let wps = 'tbd';
      if (this.setCorrect > 10) {
        wps = Math.round((this.charPerSecond * 60) / 5);
      }
      return wps;
    },
    currentSetHighCPS() {
      return this.setCorrect > 10 ? this.setHighCharsPerSecond() : 'tdb';
    },
    currentSetHighWPM() {
      return this.setCorrect > 10 ? this.setHighWordsPerMinute() : 'tdb';
    },
  },
  methods: {
    setHighCharsPerSecond() {
      let hcps = this.currentHighCPS[this.currentSet];
      if (this.charPerSecond > this.currentHighCPS[this.currentSet]) {
        this.currentHighCPS[this.currentSet] = this.charPerSecond;
        hcps = this.currentHighCPS[this.currentSet];
      }
      return hcps;
    },
    setHighWordsPerMinute() {
      let hwpm = this.currentHighWPM[this.currentSet];
      if (this.wordsPerMinute > localStorage.getItem(`${this.setName}: high WPM`)) {
        this.currentHighWPM[this.currentSet] = this.wordsPerMinute;
        hwpm = this.currentHighWPM[this.currentSet];
        localStorage.setItem(`${this.setName}: high WPM`, hwpm);
        this.setDataHWPM();
      }
      return hwpm;
    },
    setDataHWPM() {
      this.currentSetLocalHighWPM = localStorage.getItem(`${this.setName}: high WPM`);
    },
  },
  mounted() {
    this.setDataHWPM();
  },
  watch: {
    currentSet() {
      this.setDataHWPM();
    },
    wordsPerMinute() {
      this.setHighWordsPerMinute();
    },
    charPerSecond() {
      this.setHighCharsPerSecond();
    },
  },
};
</script>

<style lang="scss" scoped>
div {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}
</style>
