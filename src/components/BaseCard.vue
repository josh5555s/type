<template>
  <div class="primary-card">
    <header>
      <div class="header-container">
        <slot name='header'></slot>
      </div>
    </header>
    <slot></slot>
  </div>
</template>

<style scoped>

header {
  background-color: lightgray;
  border-radius: 8px;
  display: flex;
  justify-content: center;
}

.header-container {
  text-align: center;
}

.primary-card {
  background-color: silver;
  margin: 2rem auto;
  max-width: 50rem;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}

</style>