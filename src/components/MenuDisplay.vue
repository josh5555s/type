<template>
  <BaseCard v-if='menuActive'>
    <template #header>
      <h1> MENU </h1>
    </template>
    <template #default>
      <h1>Press (m) to toggle menu display</h1>
      <h1>Press (c) to cycle through colors</h1>
      <h1>Press (n) to move to the next character set</h1>
      <h1>Current Character Set: {{ charGroups[selectedCharGroup].toUpperCase() }}</h1>
    </template>
  </BaseCard>
</template>

<script>

import BaseCard from './BaseCard.vue'

export default {
  components: {
    BaseCard
  },
  props: ['selectedCharGroup', 'menuActive','charGroups'],
  emits: ['selectedCharGroup'],
  data: () => ({
  }),
  methods: {
    switchSelection() {
      this.$emit('next-char-set')
    },
    cycleColor() {
      this.$emit('cycle-color')
    },
    toggleMenu() {
      this.$emit('toggle-menu')
    }
  },
  mounted() {
    document.addEventListener("keypress", event => {
      if (event.key === 'm') {this.toggleMenu(event)}
      if (event.key === 'c') {this.cycleColor(event)}
      if (event.key === 'n') {this.switchSelection(event)}
    })
  }
};
</script>