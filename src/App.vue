<script setup>
import { ref } from 'vue';
import Timer from './components/Timer.vue'
import AddTimer from './components/AddTimer.vue'

const numberOfTimers = ref(3)

const addTimer = () => {
  numberOfTimers.value++
}

const deleteLastTimer = () => {
  if(numberOfTimers.value > 3) {
    numberOfTimers.value--
  }
}

</script>

<template>
  <div class="app">
    <div v-for="n in numberOfTimers">
      <Timer @dblclick="deleteLastTimer"/>
    </div>
    <AddTimer @addTimer="addTimer" />
    <div class="empty"></div>
    <div class="empty"></div>
  </div>
</template>

<style scoped>
.empty {
  width: 225px;
}
</style>
