<template>
  <ul class="container">
    <li 
      v-for="(item, i) in charArr" 
      :key="i" 
      class="vert-contain">
      <div 
        v-bind:id="'b' + i"
        class="box"
        ><h2>
          {{ item }}
        </h2>
      </div>
    </li>
  </ul>
</template>

<script>

export default {
  props: ['selectedCharGroup'],
  data: () => ({
    charArr: ['','','','','0','1','2','3','4'], 
    lastSpace: false,
    char: ''
  }),
  methods: {
    randomChar(totalPossible) {
      this.char = Math.floor(Math.random() * totalPossible)
      if (this.selectedCharGroup === 1) { this.char += 10 }
      else if (this.selectedCharGroup === 2) { this.char += 20 }
      else if (this.selectedCharGroup === 3) { this.char += 31 }
      else if (this.selectedCharGroup === 4) { this.char += 20 }
      else if (this.selectedCharGroup === 5) { this.char += 10 }
      this.char = this.char.toString()
      console.log(this.char)
    },
    randomSpace() {
      let space = Math.random()
      console.log(space)
      if (space <= 0.15 && this.lastSpace === false) {
        this.char = ' '
        this.lastSpace = true
      } else {this.lastSpace = false}
    },
    nextChar() {
      if (this.selectedCharGroup === 0 || this.selectedCharGroup === 1) { this.randomChar(10) }
      else if (this.selectedCharGroup === 2 || this.selectedCharGroup === 3) { this.randomChar(11) }
      else if (this.selectedCharGroup === 4) {this.randomChar(22)}
      else if (this.selectedCharGroup === 5) {this.randomChar(32)}
      else if (this.selectedCharGroup === 6) {this.randomChar(42)}
      if (this.char === '10') this.char = ')'
      if (this.char === '11') this.char = '!'
      if (this.char === '12') this.char = '@'
      if (this.char === '13') this.char = '#'
      if (this.char === '14') this.char = '$'
      if (this.char === '15') this.char = '%'
      if (this.char === '16') this.char = '^'
      if (this.char === '17') this.char = '&'
      if (this.char === '18') this.char = '*'
      if (this.char === '19') this.char = '('
      if (this.char === '20') this.char = '.'
      if (this.char === '21') this.char = '`'
      if (this.char === '22') this.char = '-'
      if (this.char === '23') this.char = '='
      if (this.char === '24') this.char = '['
      if (this.char === '25') this.char = ']'
      if (this.char === '26') this.char = '\\'
      if (this.char === '27') this.char = ';'
      if (this.char === '28') this.char = `'`
      if (this.char === '29') this.char = ','
      if (this.char === '30') this.char = '/'
      if (this.char === '31') this.char = '~'
      if (this.char === '32') this.char = '_'
      if (this.char === '33') this.char = '+'
      if (this.char === '34') this.char = '{'
      if (this.char === '35') this.char = '}'
      if (this.char === '36') this.char = '|'
      if (this.char === '37') this.char = ':'
      if (this.char === '38') this.char = '"'
      if (this.char === '39') this.char = `<`
      if (this.char === '40') this.char = '>'
      if (this.char === '41') this.char = '?'
      console.log(`selectedCharGroup: ${this.selectedCharGroup}`)
      this.randomSpace()
      this.charArr.shift()
      this.charArr.push(this.char)
    },
    checkMatch(event) {
      if (event.key === this.charArr[4]) {
        console.log('match!')
        this.nextChar()
      }
    },
  },
  watch: {
  },
  mounted() {
    document.addEventListener("keypress", event => {
      this.checkMatch(event)
    })
    document.querySelector('html').style.overflow="hidden"
  }
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
  background-color:darkgrey;
  box-shadow: 0px 1px 4px rgba(0, 0, 0, .1);
  height: 100px;
  width: 100px;
  margin: 20px 10px;
  padding-top: 5px;
  font-size: 40px;
  text-align: center;
  
  &#b0, &#b1, &#b2, &#b3 {
    color: grey;
  }

  &#b4 {
    background-color: snow;
    height: 120px;
    width: 120px;
    font-size: 48px;
  }
}



</style>