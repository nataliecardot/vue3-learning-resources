<template>
<!-- Using teleport feature so not deeply nested in DOM (it's being moved to end of body) - for accessibility/HTML structure -->
<teleport to="body">
  <div @click="$emit('close')"></div>
  <!-- HTML 5.2 introduced dialog element - for a modal dialog. Dialog is hidden from view by default (and from DOM access) unless open attribute is used -->
  <dialog open>
    <header>
      <!-- When you have two slots, one slot may remain unnamed, but all other slots need names -->
      <slot name="header">
        <!-- Default fallback content if no header provided -->
        <h2>{{ title }}</h2>
      </slot>
    </header>
    <section>
      <slot></slot>
    </section>
    <menu>
      <slot name="actions">
        <base-button @click="$emit('close')">Close</base-button>
      </slot>
    </menu>
  </dialog>
  </teleport>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: false
    }
  },
  emits: ['close']
}
</script>

<style scoped>
div {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.75);
  z-index: 10;
}

dialog {
  position: fixed;
  top: 20vh;
  left: 10%;
  width: 80%;
  z-index: 100;
  border-radius: 12px;
  border: none;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 0;
  margin: 0;
  overflow: hidden;
}

header {
  background-color: #3a0061;
  color: white;
  width: 100%;
  padding: 1rem;
}

header h2 {
  margin: 0;
}

section {
  padding: 1rem;
}

menu {
  padding: 1rem;
  display: flex;
  justify-content: flex-end;
  margin: 0;
}

@media (min-width: 768px) {
  dialog {
    left: calc(50% - 20rem);
    width: 40rem;
  }
}
</style>