## Intervalo

<div v-if="counter > 0">
  Pausa de
  {{ Math.floor(counter / 60).toString().padStart(2, '0') }}:{{ (counter % 60).toString().padStart(2, '0') }}
  minutos.
</div>
<div v-else>
  Time's up!
</div>

<button class="btn-default" @click="resetCounter">Reiniciar</button>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const counter = ref(300)
const timerInterval = ref(null)

const resetCounter = () => {
  counter.value = 300
  clearInterval(timerInterval.value)
  timerInterval.value = setInterval(() => {
    if (counter.value > 0) {
      counter.value--
    } else {
      clearInterval(timerInterval.value)
    }
  }, 1000)
}

onMounted(() => {
  resetCounter()
})

onUnmounted(() => {
  clearInterval(timerInterval.value)
})
</script>
