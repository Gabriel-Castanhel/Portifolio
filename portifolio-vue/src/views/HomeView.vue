<script setup lang="ts">
import Card from '../components/cards/Card.vue'
import Footer from '../components/footer/Footer.vue'
import Perfil from '../components/perfil/MiiPerfil.vue'

// Criamos um array simples para gerar os 12 cards via v-for
const channels = Array.from({ length: 12 }, (_, i) => ({
  id: i,
  title: '+',
}))
</script>

<template>
  <div class="main-wrapper">
    <main class="container-home">
      <div class="content-area">
        <div class="wii-menu-container">
          <div class="wii-grid">
            <Card v-for="channel in channels" :key="channel.id" :title="channel.title" />
          </div>
        </div>
      </div>

      <Footer class="wii-footer" />
    </main>
  </div>
</template>

<style scoped>
.wii-menu-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 20px;
}

.wii-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  width: 80%;
}

.main-wrapper {
  background-color: #ececec;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  overflow-x: hidden; /* Evita scroll horizontal indesejado */
}

.container-home {
  display: flex;
  flex-direction: column;
  flex-grow: 1; /* Faz este container ocupar o espaço restante */
  justify-content: space-between; /* Garante o Footer no fundo */
  align-items: center;
  width: 100%;
}

.content-area {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-grow: 1;
  width: 100%;
}

/* Estilização extra para o Footer se comportar como o menu do Wii */
.wii-footer {
  width: 100%;
  margin-top: auto; /* Força para o final */
}

/* Responsividade para o Container Principal */
@media (max-width: 768px) {
  .container-home {
    padding-top: 10px;
    height: auto; /* Em telas pequenas, o conteúdo define a altura */
  }
}
</style>
