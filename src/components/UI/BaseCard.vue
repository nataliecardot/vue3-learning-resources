<template>
  <div>
    <!-- This card should be used as a wrapper around any content. With a slot, can feed in any HTML and will be wrapped with div with style specified in this component
 -->
    <slot></slot>
  </div>
</template>

<style scoped>
div {
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  margin: 2rem auto;
  max-width: 40rem;
}
</style>