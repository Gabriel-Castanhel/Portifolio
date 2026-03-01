<script setup lang="ts">
// Você pode adicionar funções para os botões aqui
const openSettings = () => console.log('Abrindo Opções do Wii...');
const openMessages = () => console.log('Abrindo Mural de Mensagens...');
</script>

<template>
  <footer class="wii-footer-container">
    <div class="wii-footer-bar">
      <button class="wii-round-btn left" @click="openSettings">
        <div class="btn-inner">Wii</div>
      </button>

      <div class="wii-info-center">
        <span class="wii-date">28/02</span>
      </div>

      <button class="wii-round-btn right" @click="openMessages">
        <div class="btn-inner email-icon"></div>
      </button>
    </div>
  </footer>
</template>

<style scoped>
.wii-footer-container {
  width: 100%;
  display: flex;
  justify-content: center;
  padding-bottom: 20px;
  pointer-events: none; /* Garante que o clique passe para o fundo se necessário */
}

.wii-footer-bar {
  width: 90%;
  max-width: 1000px;
  height: 80px;
  background: linear-gradient(to bottom, #ffffff 0%, #e6e6e6 100%);
  border: 3px solid #d1d1d1;
  border-radius: 50px; /* Bordas bem redondas clássicas */
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 10px;
  box-shadow: 0 10px 20px rgba(0,0,0,0.1);
  pointer-events: auto; /* Reativa os cliques nos botões */
  position: relative;
}

/* Botões Circulares */
.wii-round-btn {
  width: 65px;
  height: 65px;
  border-radius: 50%;
  border: 2px solid #ccc;
  background: radial-gradient(circle, #fff 0%, #f0f0f0 100%);
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: inset 0 2px 5px rgba(255,255,255,0.8), 0 2px 4px rgba(0,0,0,0.1);
  transition: all 0.2s ease;
}

.wii-round-btn:hover {
  transform: scale(1.1);
  border-color: #3498db;
  box-shadow: 0 0 15px rgba(52, 152, 219, 0.4);
}

.wii-round-btn:active {
  transform: scale(0.9);
  background: #e0e0e0;
}

/* Texto interno do botão "Wii" */
.btn-inner {
  font-family: 'Arial Black', sans-serif;
  color: #888;
  font-size: 14px;
  letter-spacing: -1px;
}

/* Ícone de carta simplificado para o lado direito */
.email-icon {
  width: 20px;
  height: 14px;
  border: 2px solid #888;
  position: relative;
}
.email-icon::after {
  content: "";
  position: absolute;
  top: 0; left: 3px;
  width: 10px; height: 10px;
  border-right: 2px solid #888;
  border-bottom: 2px solid #888;
  transform: rotate(45deg) skew(10deg, 10deg);
}

/* Relógio/Data Central */
.wii-info-center {
  color: #999;
  font-weight: bold;
  font-size: 1.2rem;
  font-family: sans-serif;
}

/* Responsividade */
@media (max-width: 600px) {
  .wii-footer-bar {
    height: 60px;
  }
  .wii-round-btn {
    width: 45px;
    height: 45px;
  }
  .btn-inner { font-size: 10px; }
}
</style>