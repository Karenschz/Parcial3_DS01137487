<template>
    <dialog class="modal" :open="open">
      <div class="modal-box bg-black-100">
        <h3 class="font-bold text-lg text-black-600">¿Eliminar Tarea?</h3>
        <p class="py-4">¿Estás seguro de que deseas eliminar la tarea <strong>"{{ tareaNombre }}"</strong>? Esta acción no se puede deshacer.</p>
        
        <div class="modal-action flex justify-end">
          <button @click="$emit('close')" class="btn">Cancelar</button>
<button @click="confirmDelete" class="btn btn-error">Eliminar</button>
        </div>
      </div>
    </dialog>
  
    <div
      v-if="open"
      class="modal-backdrop fixed top-0 left-0 z-10 bg-black opacity-40 w-screen h-screen"
    ></div>
  </template>
  
  <script lang="ts" setup>
import { defineProps, defineEmits } from 'vue';
  
  interface Props {
    open: boolean;
    tareaNombre: string;
  }
const props = defineProps<Props>();
  
  const emit = defineEmits<{
    close: [];
    delete: [];
  }>();
  
  const confirmDelete = () => {
    emit('delete');
    emit('close');
  };
  </script>
  
  <style scoped>
.modal {
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 20;
}
.modal-box {
  background-color: #red; 
  padding: 20px;
  border-radius: 8px;
  max-width: 400px;
  width: 90%;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
  background-color: green;
  width: 100%;
  height: 100%;
}
</style>





