<script setup lang="ts">
import { ref, computed, type CSSProperties } from 'vue'

interface Props {
  isActive?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  isActive: false,
})

const isExpanded = ref(false)

const expand = () => {
  if (!isExpanded.value) isExpanded.value = true
}

const close = () => {
  isExpanded.value = false
}

const expansionStyles = computed((): CSSProperties => {
  const wiiEasing = 'cubic-bezier(0.16, 1, 0.3, 1)'

  if (!isExpanded.value) {
    return {
      zIndex: 1,
      transition: `all 0.6s ${wiiEasing}`,
    }
  }

  return {
    position: 'fixed',
    top: '0',
    left: '0',
    width: '100vw',
    height: '100vh',
    zIndex: 9999,
    margin: '0',
    borderRadius: '0',
    cursor: 'default',
    transform: 'scale(1)',
    transition: `all 0.8s ${wiiEasing}`,
    background: 'white',
  }
})
</script>

<template>
  <div class="card-container" :class="{ placeholder: isExpanded }">
    <div
      class="wii-card"
      :class="{ 'is-active': isActive, expanded: isExpanded }"
      :style="expansionStyles"
      @click="expand"
    >
      <div class="wii-gloss"></div>

      <div class="card-content">
        <Transition name="wii-fade">
          <div v-if="isExpanded" :key="'full'" class="expanded-view">
            <div class="content-wrapper">
              <slot name="details">
                <h1>Conteúdo do Projeto</h1>
              </slot>
              <button class="close-btn" @click.stop="close">Voltar</button>
            </div>
          </div>

          <div v-else :key="'thumb'" class="thumb-view">
            <slot name="thumb"></slot>
          </div>
        </Transition>
      </div>

      <div class="inner-frame"></div>
    </div>
  </div>
</template>

<style scoped>
.card-container {
  aspect-ratio: 1.6 / 1;
  width: 100%;
}

.wii-card {
  position: relative;
  width: 100%;
  height: 100%;
  background: white;
  border: 4px solid #dcdcdc;
  border-radius: 18px;
  cursor: pointer;
  overflow: hidden;
  display: flex;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
}

/* Transição suave entre Thumb e Detalhes */
.wii-fade-enter-active,
.wii-fade-leave-active {
  transition: opacity 0.4s ease;
  position: absolute;
  width: 100%;
  height: 100%;
}

.wii-fade-enter-from,
.wii-fade-leave-to {
  opacity: 0;
}

.thumb-view,
.expanded-view {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.content-wrapper {
  max-width: 900px;
  width: 100%;
  padding: 40px;
  animation: slideIn 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

@keyframes slideIn {
  from {
    transform: translateY(40px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.close-btn {
  margin-top: 40px;
  padding: 12px 60px;
  border-radius: 30px;
  border: 2px solid #ccc;
  background: white;
  cursor: pointer;
  font-weight: bold;
  color: #666;
  transition: 0.3s;
}

.close-btn:hover {
  background: #00e5ff;
  color: white;
  border-color: #00e5ff;
}

.wii-card:not(.expanded):hover {
  transform: scale(1.05);
  border-color: #00e5ff;
}

.wii-gloss {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 48%;
  background: linear-gradient(to bottom, rgba(255, 255, 255, 0.7) 0%, rgba(255, 255, 255, 0) 100%);
  pointer-events: none;
  z-index: 10;
}

.card-content {
  width: 100%;
  height: 100%;
  z-index: 2;
  position: relative;
}

.inner-frame {
  position: absolute;
  top: 4%;
  left: 3%;
  right: 3%;
  bottom: 4%;
  border: 1px solid rgba(0, 0, 0, 0.05);
  border-radius: 14px;
  pointer-events: none;
  z-index: 1;
}
</style>
