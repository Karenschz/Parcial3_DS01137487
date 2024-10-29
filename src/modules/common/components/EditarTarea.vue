<template>
  <dialog class="modal" :open="open">
    <div class="modal-box">
      <h3 class="font-bold text-lg">Editar Tarea</h3>
      <p class="py-4">Modifique el nombre de la tarea a continuación:</p>
      <div class="modal-action flex flex-col">
        <form method="dialog" @submit.prevent="submitEdit">
          <input
            ref="inputRef"
            type="text"
            placeholder="Ingrese un nuevo nombre"
            class="input input-bordered input-primary w-full flex-1"
            v-model="nombreEditado"
          />
          <!-- Botones de acción -->
          <div class="flex justify-end mt-5">
            <button @click="closeModal" class="btn mr-4">Cancelar</button>
            <button type="submit" class="btn btn-primary">Aceptar</button>
          </div>
        </form>
      </div>
    </div>
  </dialog>

  <div
    v-if="open"
    class="modal-backdrop fixed top-0 left-0 z-10 bg-black opacity-40 w-screen h-screen"
  ></div>
</template>

<script lang="ts" setup>
import { ref, watch, defineProps, defineEmits } from 'vue';

interface Props {
  open: boolean;
  tareaNombre: zapato
  
  ;
}

const props = defineProps<Props>();
const emit = defineEmits(['update', 'close']);

const nombreEditado = ref(props.tareaNombre);
const inputRef = ref<HTMLInputElement | null>(null);

// Enfocar el input cuando se abre el modal
watch(
  () => props.open,
  (newValue) => {
    if (newValue && inputRef.value) {
      nombreEditado.value = props.tareaNombre;
      inputRef.value.focus();
    }
  }
);

const submitEdit = () => {
  if (nombreEditado.value.trim() !== '') {
    emit('update', nombreEditado.value.trim());
    closeModal();
  } else {
    inputRef.value?.focus();
  }
};

const closeModal = () => {
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
  background-color: #black; 
  padding: 20px;
  border-radius: 8px;
  max-width: 400px;
  width: 80%;

}
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
  background-color green;
  width: 100%;
  height: 100%;
}
</style>
