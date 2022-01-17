<template>
  <v-app>
    <div :class="theme" class="full-screen">
      <div class="body">
        <Menu-Display
          :class="theme"
          :theme="theme"
          :menuActive="menuActive"
          :selectedCharGroup="selectedCharGroup"
          :charGroups="charGroups"
          @toggle-menu="toggleMenu"
          @toggle-stats="toggleStats"
          @next-char-set="switchCharSet"
          @cycle-color="cycleColor"
        />
        <char-display
          :theme="theme"
          :charGroups="charGroups"
          :selectedCharGroup="selectedCharGroup"
        />
        <Stats-Display v-if="statsActive" />
      </div>
    </div>
  </v-app>
</template>

<script>
import MenuDisplay from './components/MenuDisplay.vue';
import CharDisplay from './components/CharDisplay.vue';
import StatsDisplay from './components/StatsDisplay.vue';

export default {
  name: 'App',

  components: {
    MenuDisplay,
    CharDisplay,
    StatsDisplay,
  },

  data: () => ({
    themeIndex: 0,
    themes: [
      'theme-green',
      'theme-blue',
      'theme-lime',
      'theme-amber',
      'theme-gray',
    ],
    selectedCharGroup: 0,
    menuActive: true,
    statsActive: true,
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
      return this.themes[this.themeIndex];
    },
  },
  methods: {
    toggleMenu() {
      this.menuActive = !this.menuActive;
    },
    toggleStats() {
      this.statsActive = !this.statsActive;
    },
    switchCharSet() {
      this.selectedCharGroup++;
      if (this.selectedCharGroup === this.charGroups.length) {
        this.selectedCharGroup = 0;
      }
    },
    cycleColor() {
      this.themeIndex++;
      if (this.themeIndex === this.themes.length) this.themeIndex = 0;
    },
  },
  watch: {
    theme() {
      console.log(this.theme);
    },
  },
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
  &#b0,
  &#b1,
  &#b2,
  &#b3 {
    color: grey;
  }
}

.theme-blue.full-screen {
  background-color: #1e88e5; // blue darken-1
}

.theme-blue.primary-card {
  background-color: #42a5f5; // blue lighten-1
}

.theme-blue header {
  background-color: #64b5f6; // blue lighten-2
}

.theme-blue.box {
  background-color: #64b5f6; // blue lighten-2
}

.theme-blue.box#b4 {
  background-color: #bbdefb; // blue lighten-4
}

.theme-blue.box {
  &#b0,
  &#b1,
  &#b2,
  &#b3 {
    background-color: #42a5f5; // blue lighten-1
    color: #1e88e5; // blue darken-1
  }
}

.theme-green.full-screen {
  background-color: #43a047; // green darken-1
}

.theme-green.primary-card {
  background-color: #66bb6a; // green lighten-1
}

.theme-green header {
  background-color: #81c784; // green lighten-2
}

.theme-green.box {
  background-color: #81c784; // green lighten-2
}

.theme-green.box#b4 {
  background-color: #c8e6c9; // green lighten-4
}

.theme-green.box {
  &#b0,
  &#b1,
  &#b2,
  &#b3 {
    background-color: #66bb6a; // green lighten-1
    color: #43a047; // green darken-1
  }
}

.theme-amber.full-screen {
  background-color: #ffc107; // amber
}

.theme-amber.primary-card {
  background-color: #ffca28; // amber lighten-1
}

.theme-amber header {
  background-color: #ffd54f; // amber lighten-2
}

.theme-amber.box {
  background-color: #ffd54f; // amber lighten-2
}

.theme-amber.box#b4 {
  background-color: #ffecb3; // amber lighten-4
}

.theme-amber.box {
  &#b0,
  &#b1,
  &#b2,
  &#b3 {
    background-color: #ffca28; // amber lighten-1
    color: #ffc107; // amber
  }
}

.theme-lime.full-screen {
  background-color: #cddc39; // lime
}

.theme-lime.primary-card {
  background-color: #d4e157; // lime lighten-1
}

.theme-lime header {
  background-color: #dce775; // lime lighten-2
}

.theme-lime.box {
  background-color: #dce775; // lime lighten-2
}

.theme-lime.box#b4 {
  background-color: #f0f4c3; // lime lighten-4
}

.theme-lime.box {
  &#b0,
  &#b1,
  &#b2,
  &#b3 {
    background-color: #d4e157; // lime lighten-1
    color: #cddc39; // lime
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
