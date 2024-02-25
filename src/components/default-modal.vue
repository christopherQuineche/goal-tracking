<template>

    <transition name="fade">
      <div class="modal-overlay" v-if="open"></div>
    </transition>

    <transition name="modal">
        <div class="modal-overlay" v-if="open">
            <div class="modal" v-if="open">
                <div class="modal-content">
                    <div class="modal-header">
                        <h2>{{ title }}</h2>
                        <button @click="$emit('close')">X</button>
                    </div>

                    <div class="modal-body">
                        <slot></slot>
                    </div>
            
                    <div class="modal-footer">
                        <button @click="$emit('confirm')">{{ textConfirm }}</button>
                    </div>
                </div>
            </div>
        </div>
    </transition>
    
</template>

<script>
export default {
    name: 'default-modal',

    props: {
        open: {
			default: false,
			type: Boolean,
		},
        textConfirm: {
            type: String,
            default: 'Aceptar'
        },
    },
};
</script>

<style lang="scss" scoped>

/* Estilos para el modal overlay */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(51, 51, 51, 0.26);
}

/* Estilos para el modal */
.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 9999;
}
/* Estilos para el contenido del modal */
.modal-content {
  background-color: black;
  padding: 20px;
  width: 400px;
  color: white;
  border-radius: 20px;
  border: 1px solid #646cff;
  transition: 0.5s;
  filter: drop-shadow(0 0 0.5em #646cff);
}

.modal-content:hover {
  border: 2px solid #444dfa;  
  transition: 0.5s;
  filter: drop-shadow(0 0 0.6em #444dfa);
}

/* Resto de estilos para el modal (header, body, footer, etc.) */
.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.modal-header h2 {
  margin: 0;
}
.modal-header button {
  background: none;
  border: none;
  font-size: 18px;
  cursor: pointer;
  color: white; 
}
.modal-body {
  margin-bottom: 20px;
}
.modal-footer {
  display: flex;
  justify-content: center;
}
.modal-footer button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}
.modal-footer button:hover {
  background-color: #0056b3;
}

/* Animaciones */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
.modal-enter-active, .modal-leave-active {
  transition: opacity 0.2s, transform 0.2s;
}
.modal-enter, .modal-leave-to {
  opacity: 0;
  transform: scale(0.7);
}
</style>