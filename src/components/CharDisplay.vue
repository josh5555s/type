<template>
  <ul class="container">
    <li v-for="(item, i) in displayArr" :key="i" class="vert-contain">
      <div v-bind:id="'b' + i" :class="theme" class="box">
        <h2>
          {{ item }}
        </h2>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: ['theme', 'currentSet'],
  emits: ['char-archive'],
  data: () => ({
    displayArr: [],
    numbersArr: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
    numberSymbolsArr: [')', '!', '@', '#', '$', '%', '^', '&', '*', '('],
    otherSymbolsNoShiftArr: ['.', '`', '-', '=', '[', ']', '\\', ';', `'`, ',', '/'],
    otherSymbolsShiftArr: ['>', '~', '_', '+', '{', '}', '|', ':', '"', '<', '?'],
    lastSpace: false,
    char: '',
    typingStarted: false,
    timeBegins: 0,
    charErrorCount: 0,
  }),
  computed: {
    allOtherSymbolsArr() {
      return this.otherSymbolsNoShiftArr.concat(this.otherSymbolsShiftArr);
    },
    allSymbolsArr() {
      return this.numberSymbolsArr.concat(this.allOtherSymbolsArr);
    },
    allSymbolsAndNumbersArr() {
      return this.allSymbolsArr.concat(this.numbersArr);
    },
  },

  methods: {
    setDisplayArr() {
      this.displayArr = ['', '', '', '', '', '', '', '', ''];
      [1, 2, 3, 4, 5].forEach(() => {
        this.char = this.getChar();
        this.displayArr.push(this.char);
        this.displayArr.shift();
      });
    },
    getChar() {
      if (this.currentSet === 0) {
        return this.numbersArr[Math.floor(Math.random() * this.numbersArr.length)];
      } else if (this.currentSet === 1) {
        return this.numberSymbolsArr[
          Math.floor(Math.random() * this.numberSymbolsArr.length)
        ];
      } else if (this.currentSet === 2) {
        return this.otherSymbolsNoShiftArr[
          Math.floor(Math.random() * this.otherSymbolsNoShiftArr.length)
        ];
      } else if (this.currentSet === 3) {
        return this.otherSymbolsShiftArr[
          Math.floor(Math.random() * this.otherSymbolsShiftArr.length)
        ];
      } else if (this.currentSet === 4) {
        return this.allOtherSymbolsArr[
          Math.floor(Math.random() * this.allOtherSymbolsArr.length)
        ];
      } else if (this.currentSet === 5) {
        return this.allSymbolsArr[Math.floor(Math.random() * this.allSymbolsArr.length)];
      } else if (this.currentSet === 6) {
        return this.allSymbolsAndNumbersArr[
          Math.floor(Math.random() * this.allSymbolsAndNumbersArr.length)
        ];
      }
    },
    randomSpace() {
      let space = Math.random();
      if (space <= 0.18 && this.lastSpace === false) {
        this.char = ' ';
        this.lastSpace = true;
      } else {
        this.lastSpace = false;
      }
    },
    checkMatch(event) {
      const menuChars = ['m', 's', 'c', 'n'];
      const isMenuKey = menuChars.includes(event.key);
      if (event.key === this.displayArr[4]) {
        this.keyWasCorrect(event.key);
        this.typingStarted = true;
        this.timeBegins = Date.now();
      } else if (!isMenuKey) {
        this.charErrorCount++;
      }
    },
    keyWasCorrect(eventKey) {
      this.$emit('char-archive', {
        char: eventKey,
        charSet: this.currentSet,
        errorCount: this.charErrorCount,
        time: Date.now() - this.timeBegins,
      });
      this.charErrorCount = 0;
      this.displayArr.shift(), (this.char = this.getChar());
      this.randomSpace();
      this.displayArr.push(this.char);
    },
  },
  watch: {
    currentSet() {
      this.setDisplayArr();
    },
  },
  mounted() {
    this.setDisplayArr();
    document.addEventListener('keypress', (event) => {
      this.checkMatch(event);
    });
    document.querySelector('html').style.overflow = 'hidden';
  },
};
</script>
<style lang="scss" scoped>
.container {
  /* background-color:darkslategrey; */
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.vert-contain {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.box {
  box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.1);
  height: 100px;
  width: 100px;
  margin: 20px 10px;
  padding-top: 5px;
  font-size: 40px;
  text-align: center;

  &#b4 {
    height: 120px;
    width: 120px;
    font-size: 48px;
  }
}
</style>
