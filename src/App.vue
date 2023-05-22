<template>
  <button @click="toggle()" id="toggleBtn">Открыть окно</button>
  <ModalWindow @show="toggle" v-if="visibleForm"/>
</template>

<script>
import ModalWindow from './components/ModalWindow.vue'

export default {
  name: 'App',
  data() {
    return {
      visibleForm: false,
    }
  },
  methods: {
    toggle() {
      this.visibleForm = !this.visibleForm;
    },
  },
  components: {
    ModalWindow
  },
  emits: ['toggle']
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#toggleBtn {
  margin-bottom: 1rem;
}
</style>
