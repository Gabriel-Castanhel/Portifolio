<script setup lang="ts">
interface Props {
  title?: string
  image?: string
  isActive?: boolean
}

// Definindo props para que cada card possa ter seu próprio conteúdo
const props = withDefaults(defineProps<Props>(), {
  title: '+',
  image: '',
  isActive: false,
})
</script>

<template>
  <div class="wii-card" :class="{ 'is-active': isActive }">
    <div class="wii-gloss"></div>

    <div class="card-content">
      <img v-if="image" :src="image" :alt="title" class="channel-image" />
      <span v-else class="channel-text">{{ title }}</span>
    </div>

    <div class="inner-frame"></div>
  </div>
</template>

<style scoped>
.wii-card {
  position: relative;
  aspect-ratio: 1.6 / 1;
  background: linear-gradient(180deg, #ffffff 0%, #f5f5f5 40%, #e0e0e0 100%);
  border: 4px solid #dcdcdc;
  border-radius: 18px;
  cursor: pointer;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  box-shadow:
    0 5px 15px rgba(0, 0, 0, 0.08),
    inset 0 2px 5px rgba(255, 255, 255, 1);
}

/* Efeito de Seleção (Azul do Wii) */
.wii-card:hover {
  transform: scale(1.08);
  border-color: #4cb3ff;
  box-shadow: 0 0 20px rgba(76, 179, 255, 0.6);
  z-index: 5;
}

.wii-card:active {
  transform: scale(0.95);
  filter: brightness(0.9);
}

/* Brilho Convexo (Efeito de Vidro) */
.wii-gloss {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 50%;
  background: linear-gradient(
    to bottom,
    rgba(255, 255, 255, 0.5) 0%,
    rgba(255, 255, 255, 0.05) 100%
  );

  pointer-events: none;
  z-index: 3;
}

/* Conteúdo (Imagem ou Texto) */
.card-content {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px;
  z-index: 2;
  user-select: none;
}

.channel-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 8px;
}

.channel-text {
  color: #999;
  font-family: 'Arial Rounded MT Bold', 'Helvetica', sans-serif;
  font-size: 1.5rem;
  font-weight: bold;
  text-shadow: 1px 1px 0px #fff;
}

/* Moldura interna para dar profundidade */
.inner-frame {
  position: absolute;
  top: 6%;
  left: 4%;
  right: 4%;
  bottom: 6%;
  border: 1px solid rgba(0, 0, 0, 0.03);
  border-radius: 12px;
  pointer-events: none;
  z-index: 1;
}

/* Estilo para o canal que está "Ativo" (opcional) */
.is-active {
  border-color: #4cb3ff;
}
</style>
