<script setup lang="ts">
withDefaults(defineProps<{
  gap?: string
  show?: boolean
}>(), {
  gap: '16px'
})

defineEmits<{
  (e: 'close'): void
  (e: 'backdrop'): void
}>()
</script>

<template>
  <Teleport to="body">
    <Transition name="modal">
      <div v-if="show" class="modal-backdrop" @click="$emit('backdrop')">
        <div class="modal" :style="{ '--gap': gap }" @click.stop>
          <button class="modal__close-btn" @click="$emit('close')">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="20px" height="20px" fill="currentColor">
              <path d="M 4.9902344 3.9902344 A 1.0001 1.0001 0 0 0 4.2929688 5.7070312 L 10.585938 12 L 4.2929688 18.292969 A 1.0001 1.0001 0 1 0 5.7070312 19.707031 L 12 13.414062 L 18.292969 19.707031 A 1.0001 1.0001 0 1 0 19.707031 18.292969 L 13.414062 12 L 19.707031 5.7070312 A 1.0001 1.0001 0 0 0 18.980469 3.9902344 A 1.0001 1.0001 0 0 0 18.292969 4.2929688 L 12 10.585938 L 5.7070312 4.2929688 A 1.0001 1.0001 0 0 0 4.9902344 3.9902344 z"/>
            </svg>
          </button>
          <div class="modal__header">
            <slot name="header"></slot>
          </div>
          <div class="modal__body">
            <slot></slot>
          </div>
          <div class="modal__footer">
            <slot name="footer"></slot>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<style lang="scss">
.modal-backdrop {
  align-items: center;
  background-color: hsla(0, 0%, 0%, .2);
  display: grid;
  height: 100%;
  left: 0;
  overflow: auto;
  position: fixed;
  top: 0;
  transition: .15s opacity;
  width: 100%;
  z-index: 2023;

  .modal {
    background-color: hsl(0, 0%, 100%);
    border-radius: 8px;
    box-shadow: 3px 3px 15px hsl(0, 0%, 67%);
    display: flex;
    flex-direction: column;
    gap: var(--gap);
    margin: 32px auto;
    min-width: 300px;
    padding: var(--gap);
    position: relative;
    transition: .15s transform;

    .modal__close-btn {
      background-color: hsl(0, 0%, 95%);
      border: none;
      border-radius: 4px;
      color: hsl(0, 0%, 33%);
      display: grid;
      padding: 2px;
      place-content: center;
      position: absolute;
      right: 8px;
      top: 8px;
      transition: .25s background-color;
      z-index: 2024;

      &:hover,
      &:active {
        background-color: hsl(0, 0%, 90%);
        cursor: pointer;
      }
      &:active,
      &:focus-visible {
        outline: 2px solid hsl(0, 0%, 50%);
        outline-offset: 2px;
      }
    }
    .modal__header {
      font-size: 24px;
      font-weight: bold;

      &:empty {
        display: none;
      }
    }
    .modal__footer:empty {
      display: none;
    }
  }

  &.modal-enter-from,
  &.modal-leave-to {
    opacity: 0;
  }

  &.modal-enter-from .modal,
  &.modal-leave-to .modal {
    transform: scale(1.1);
  }
}
</style>