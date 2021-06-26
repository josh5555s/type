<template>
  <v-app>
    <div class="full-screen">
      <div class="body">
        <Menu-Display
          :menuActive='menuActive'
          :selectedCharGroup='selectedCharGroup'
          :charGroups='charGroups'
          @next-char-set='switchCharSet'
          @toggle-menu='toggleMenu'
        />
        <Char-Display
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
  methods: {
    switchCharSet() {
      this.selectedCharGroup++
      if (this.selectedCharGroup === this.charGroups.length) {
        this.selectedCharGroup = 0
      }
    },
    toggleMenu() {
      this.menuActive = !this.menuActive
      console.log(this.menuActive)
    }
  },
};
</script>

<style lang="scss">

html {
  overflow: hidden;
}

.full-screen {
  background-color: gray;
  height: 100vh;
  width: 100vw;
}
div {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

</style>