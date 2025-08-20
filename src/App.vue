<script setup>
// Lógica JavaScript
import { ref, computed } from 'vue';

const tempoTotal = ref(1500);
const estaRodando = ref(false);
let timerId = null;

const minutos = computed(() => {
  const m = Math.floor(tempoTotal.value / 60);
  return m < 10 ? '0' + m : m;
});

const segundos = computed(() => {
  const s = tempoTotal.value % 60;
  return s < 10 ? '0' + s : s;
});

const iniciarTemporizador = () => {
  if (estaRodando.value) return;

  estaRodando.value = true;
  timerId = setInterval(() => {
    if (tempoTotal.value > 0) {
      tempoTotal.value--;
    } else {
      pararTemporizador();
      alert('Tempo de foco finalizado!');
    }
  }, 1000);
};

const pararTemporizador = () => {
  estaRodando.value = false;
  clearInterval(timerId);
};

const resetarTemporizador = () => {
  pararTemporizador();
  tempoTotal.value = 1500;
};
</script>

<template>
  <main class="container d-flex flex-column justify-content-center align-items-center vh-100 text-center">
    <h1>Contador de Foco</h1>
    <div class="timer-display">
      <h2>{{ minutos }}:{{ segundos }}</h2>
    </div>
    <div class="controls mt-4">
      <button class="btn btn-primary me-2" @click="iniciarTemporizador">Iniciar</button>
      <button class="btn btn-secondary me-2" @click="pararTemporizador">Pausar</button>
      <button class="btn btn-danger" @click="resetarTemporizador">Resetar</button>
    </div>
  </main>
</template>

<style scoped>
:root {
  --bg-dark: #1B2C4A;
  --accent-green: #00ff97;
  --button-green: #47cc96;
  --text-light: #E2D5CE;
}

main {
  background-color: var(--bg-dark);
  color: var(--text-light);
  border-radius: 10px;
  padding: 2rem;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.timer-display h2 {
  font-size: 5rem;
  font-weight: bold;
  color: var(--accent-green);
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.controls .btn {
  font-weight: bold;
}

.btn-primary {
  background-color: var(--button-green);
  border-color: var(--button-green);
  color: var(--bg-dark);
}

.btn-primary:hover {
  background-color: #35a076;
  border-color: #35a076;
}

.btn-secondary {
  background-color: var(--text-light);
  border-color: var(--text-light);
  color: var(--bg-dark);
}

.btn-secondary:hover {
  background-color: #d2c5bf;
  border-color: #d2c5bf;
}

.btn-danger {
  background-color: #dc3545;
  border-color: #dc3545;
}

.btn-danger:hover {
  background-color: #c82333;
  border-color: #bd2130;
}
</style>