<template>
  <v-app>
    <div :class="theme" class="full-screen">
      <div class="body">
        <Menu-Display
          :class="theme"
          :theme="theme"
          :menuActive='menuActive'
          :selectedCharGroup='selectedCharGroup'
          :charGroups='charGroups'
          @next-char-set='switchCharSet'
          @toggle-menu='toggleMenu'
          @cycle-color='cycleColor'
        />
        <Char-Display
          :theme='theme'
          :charGroups='charGroups' 
          :selectedCharGroup='selectedCharGroup'
        />
      </div>
    </div>
  </v-app>
</template>

<script>
import MenuDisplay from './components/MenuDisplay.vue'
import CharDisplay from './components/CharDisplay.vue'

export default {
  name: 'App',

  components: {
    MenuDisplay,
    CharDisplay
  },

  data: () => ({
    themeIndex: 0,
    themes: ['theme-green','theme-blue','theme-lime','theme-amber','theme-gray'],
    selectedCharGroup: 0,
    menuActive: true,
    charGroups: [
      'numbers',
      'number symbols',
      'other symbols (no shift)',
      'other symbols (shift)',
      'all other symbols',
      'all symbols',
      'all symbols and numbers',
      ],
  }),
  computed: {
    theme() {
      return this.themes[this.themeIndex]
    }
  },
  methods: {
    switchCharSet() {
      this.selectedCharGroup++
      if (this.selectedCharGroup === this.charGroups.length) {
        this.selectedCharGroup = 0
      }
    },
    cycleColor() {
     this.themeIndex++ 
     if (this.themeIndex === this.themes.length) this.themeIndex = 0
    },
    toggleMenu() {
      this.menuActive = !this.menuActive
      console.log(this.menuActive)
    }
  },
  watch: {
    theme() {
      console.log(this.theme)
    }
  }
};
</script>

<style lang="scss">

// @mixin theme($name, $color) {
//   .#{$name} {
//     .full-screen {
//       background-color: $color;
//     }
//   }
// }

// @include theme(theme-green, #4CAF50);

.theme-gray.full-screen {
  background-color: gray;
}

.theme-gray.box {
  background-color: darkgray;
}

.theme-gray.box#b4 {
  background-color: snow;
}

.theme-gray.box {
  &#b0, &#b1, &#b2, &#b3 {
    color: grey;
  }
}

.theme-blue.full-screen {
  background-color: #1E88E5; // blue darken-1
}

.theme-blue.primary-card {
  background-color: #42A5F5; // blue lighten-1
}

.theme-blue header {
  background-color: #64B5F6; // blue lighten-2
}

.theme-blue.box {
  background-color: #42A5F5; // blue lighten-1
}

.theme-blue.box#b4 {
  background-color: #BBDEFB; // blue lighten-4
}

.theme-blue.box {
  &#b0, &#b1, &#b2, &#b3 {
    color: #1E88E5; // blue darken-1
  }
}

.theme-green.full-screen {
  background-color: #43A047; // green darken-1
}

.theme-green.primary-card {
  background-color: #66BB6A; // green lighten-1
}

.theme-green header {
  background-color: #81C784; // green lighten-2
}

.theme-green.box {
  background-color: #66BB6A; // green lighten-1
}

.theme-green.box#b4 {
  background-color: #C8E6C9; // green lighten-4
}

.theme-green.box {
  &#b0, &#b1, &#b2, &#b3 {
    color: #43A047; // green darken-1
  }
}

.theme-amber.full-screen {
  background-color: #FFC107; // amber 
}

.theme-amber.primary-card {
  background-color: #FFCA28; // amber lighten-1
}

.theme-amber header {
  background-color: #FFD54F; // amber lighten-2
}

.theme-amber.box {
  background-color: #FFCA28; // amber lighten-1
}

.theme-amber.box#b4 {
  background-color:#FFECB3; // amber lighten-4
}

.theme-amber.box {
  &#b0, &#b1, &#b2, &#b3 {
    color: #FFC107; // amber
  }
}

.theme-lime.full-screen {
  background-color: #CDDC39; // lime 
}

.theme-lime.primary-card {
  background-color: #D4E157; // lime lighten-1
}

.theme-lime header {
  background-color: #DCE775; // lime lighten-2
}

.theme-lime.box {
  background-color: #D4E157; // lime lighten-1
}

.theme-lime.box#b4 {
  background-color:#F0F4C3; // lime lighten-4
}

.theme-lime.box {
  &#b0, &#b1, &#b2, &#b3 {
    color: #CDDC39; // lime
  }
}
html {
  overflow: hidden;
}

.full-screen {
  height: 100vh;
  width: 100vw;
}
div {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

</style>