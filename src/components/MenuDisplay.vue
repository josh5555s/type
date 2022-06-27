<template>
  <BaseCard v-if="menuActive">
    <template #header>
      <h1>MENU</h1>
    </template>
    <template #default>
      <h1>Press (m) to toggle menu display</h1>
      <h1>Press (s) to toggle stats display</h1>
      <h1>Press (c) to cycle through colors</h1>
      <h1>Press (n) to move to the next character set</h1>
      <h1>Current Character Set: {{ charGroups[currentSet].toUpperCase() }}</h1>
    </template>
  </BaseCard>
</template>

<script>
import BaseCard from './BaseCard.vue';

export default {
  components: {
    BaseCard,
  },
  props: ['currentSet', 'menuActive', 'charGroups'],
  emits: ['currentSet'],
  data: () => ({}),
  methods: {
    toggleMenu() {
      this.$emit('toggle-menu');
    },
    toggleStats() {
      this.$emit('toggle-stats');
    },
    cycleColor() {
      this.$emit('cycle-color');
    },
    switchSelection() {
      this.$emit('next-char-set');
    },
  },
  mounted() {
    document.addEventListener('keypress', (event) => {
      if (event.key === 'm') {
        this.toggleMenu(event);
      }
      if (event.key === 's') {
        this.toggleStats(event);
      }
      if (event.key === 'c') {
        this.cycleColor(event);
      }
      if (event.key === 'n') {
        this.switchSelection(event);
      }
    });
  },
};
</script>
