<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
const data = ref(new Date())

const formatarHora = (date: Date) => {
  return date.toLocaleTimeString('en-US', {
    hour: 'numeric',
    minute: '2-digit',
    hour12: true,
  })
}

const dataAtual = ref(new Date())

// Função para formatar a data (ex: 01/03/2026)
const formatarData = (data: Date) => {
  return data.toLocaleDateString()
}

// 2. Criamos o timer quando o componente for montado
let timer: any

onMounted(() => {
  timer = setInterval(() => {
    dataAtual.value = new Date() // Atualiza a referência a cada segundo
  }, 1000)
})

// 3. Limpamos o timer quando o componente for destruído (evita vazamento de memória)
onUnmounted(() => {
  clearInterval(timer)
})
</script>

<template>
  <footer class="wii-footer-wrapper">
    <div class="wii-wave-container">
      <svg viewBox="0 0 1000 100" preserveAspectRatio="none" class="wii-wave-svg">
        <path d="M0,100 C150,0 850,0 1000,100 L1000,100 L0,100 Z" fill="#ffffff" />
        <path d="M0,100 C150,5 850,5 1000,100" fill="none" stroke="#00e5ff" stroke-width="2" />
      </svg>
    </div>

    <div class="wii-footer-content">
      <div class="footer-section left">
        <button class="wii-main-btn">
          <span class="wii-logo">Wii</span>
        </button>
      </div>

      <div class="footer-section center">
        <div class="wii-clock-area">
          <div class="time">
            <span>{{ formatarHora(dataAtual) }}</span>
          </div>
          <div class="date">{{ formatarData(dataAtual) }}</div>
        </div>
      </div>

      <div class="footer-section right">
        <button class="wii-main-btn message-btn">
          <div class="mail-icon"></div>
        </button>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.wii-footer-wrapper {
  position: relative;
  width: 100%;
  background-color: #ffffff;
  padding-bottom: 20px;
}

/* A Curva azul do topo */
.wii-wave-container {
  position: absolute;
  top: -60px; /* Ajuste para encaixar no topo da barra branca */
  width: 100%;
  height: 60px;
}

.wii-wave-svg {
  width: 100%;
  height: 100%;
}

.wii-footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 40px;
  max-width: 1200px;
  margin: 0 auto;
}

/* Estilo dos Botões Circulares Grandes */
.wii-main-btn {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  border: 4px solid #b7f4f8; /* Azul bem clarinho */
  background: radial-gradient(circle, #ffffff 0%, #f0fbfb 100%);
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: transform 0.2s;
}

.wii-main-btn:hover {
  transform: scale(1.05);
  border-color: #00e5ff;
}

.wii-logo {
  font-weight: bold;
  font-size: 24px;
  color: #a0a0a0;
  letter-spacing: -1px;
}

/* Área Central: Relógio e SD */
.footer-section.center {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
  margin-top: -20px;
  z-index: 10;
}

.wii-clock-area {
  text-align: center;
  color: #7d7d7d;
}

.time {
  font-size: 42px;
  font-weight: 300;
  letter-spacing: 2px;
}

.am-pm {
  font-size: 16px;
  margin-left: 5px;
}

.date {
  font-size: 28px;
  font-weight: bold;
  color: #909090;
}

/* Ícone do Cartão SD */
.wii-sd-slot {
  width: 35px;
  height: 45px;
  border: 2px solid #ccc;
  border-radius: 4px;
  background: #fdfdfd;
  position: relative;
  margin-bottom: 5px;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.05);
}

.wii-sd-slot::after {
  content: 'SD';
  position: absolute;
  bottom: 2px;
  width: 100%;
  text-align: center;
  font-size: 10px;
  color: #ccc;
}

/* Ícone de Carta (Direita) */
.mail-icon {
  width: 35px;
  height: 25px;
  border: 3px solid #a0a0a0;
  border-radius: 3px;
  position: relative;
}

.mail-icon::before {
  content: '';
  position: absolute;
  top: 0;
  left: 6px;
  width: 17px;
  height: 17px;
  border-right: 3px solid #a0a0a0;
  border-bottom: 3px solid #a0a0a0;
  transform: rotate(45deg);
}

/* Responsividade */
@media (max-width: 768px) {
  .time {
    font-size: 30px;
  }
  .date {
    font-size: 20px;
  }
  .wii-main-btn {
    width: 70px;
    height: 70px;
  }
}
</style>
