<script>
import defaultModal from './default-modal.vue'; 
export default {
  data() {
    return {
      addTextActivity: '',
      addHours: null,
      listActivity: [],
      msgAlert: '',
      showModal: false,
    }
  },
  methods: {
    addActivity() {
      if(this.addTextActivity.length > 10 && this.addHours > 0){
        this.listActivity.push({
          description: this.addTextActivity,
          hours: this.addHours
        });
        this.addTextActivity = '';
        this.addHours = null;
        this.msgAlert = '';
        this.openModal();
      } else {
        if (this.addTextActivity.length < 10) {
          this.msgAlert = 'Describa mejor su actividad'
        }
        else if (this.addHours === 0 || this.addHours === null ) {
          this.msgAlert = 'Agregue las horas de su actividad'
        }
      }
    },
    openModal() {
      this.showModal = !this.showModal
      this.addTextActivity = '';
      this.addHours = null;
    }
  },
  computed: {
    totalHours() {
      return this.listActivity.reduce((total, activity) => total + activity.hours, 0);
    }
  },
  components: {
    defaultModal,
  },
}


</script>

<template>
  <div class="card-general">
    <h2>TU PROGRESO</h2>
    <div 
    class="container-list" 
    v-if="this.listActivity.length > 0"
    >
      <ul class="activity-list">
        <li 
          v-for="(list, index) in listActivity" :key="index">
            <span class="column-description">{{ list.description }}</span> <span class="column-hours">- <b>{{ list.hours }} hora(s)</b></span>
        </li>
      </ul>
      <div class="container-hours-total">
        <p><b>Horas totales: {{ totalHours }}</b></p>
      </div>
    </div>
    <h3 v-else>No hay progreso registrado</h3>

    <button
      @click="openModal">Agregar</button>
  </div>

  <defaultModal
    :open="showModal" 
    @close="openModal" 

    textConfirm="Aceptar"
    @confirm="addActivity">

    <h2 class="title-modal">Agregue un nuevo progreso</h2>
    <input 
      type="text" 
      placeholder="Progreso del día"
      v-model="addTextActivity"
      class="input-block">
    <input 
      type="text" 
      placeholder="Descripcion del progreso"
      v-model="textDescription"
      class="input-block">
    <input 
      type="number" 
      placeholder="Hora(s)"
      v-model="addHours"
      class="input-block">
    <input 
      type="text" 
      placeholder="Estado del progreso"
      v-model="state"
      class="input-block">
    <input 
      type="text" 
      placeholder="Comentarios del progreso"
      v-model="coment"
      class="input-block">

      <span style="color: red;">{{ this.msgAlert }}</span>
  </defaultModal>

</template>

<style scoped>
.card-general {
  background-color: black;
  padding: 80px;
  border-radius: 50px;
  width: 600px;
  height: 600px;
  border-top: rgb(66, 66, 66) solid 5px;
  transition: 1s;
  h2 {
    margin: 0 0 30px 0;
  }
}
.card-general:hover{
  transition: 0.5s;
  filter: drop-shadow(0 0 1.5em #1c4458);
}

button {
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 10px 20px;
  font-size: 1em;
  font-weight: 500;
  background-color: #1d1d1d;
  cursor: pointer;
  transition: border-color 0.25s;
  margin-left: 5px;
}
button:hover {
  border-color: #646cff;
}
button:focus,
button:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}
.activity-list {
  height: 420px;
  overflow-y: auto;
  scrollbar-width: thin;
  text-align: start;
  .column-description {
    font-size: 15px;
    display: inline-block;
    width: 400px; /* Establece el ancho máximo */
    overflow: hidden; /* Controla el desbordamiento */
    white-space: nowrap; /* Evita que el texto se envuelva */
    text-overflow: ellipsis; /* Agrega puntos suspensivos cuando el texto excede el ancho */
  }
}

.input-block {
  display: block;
  margin: 0 auto 20px;
  width: 70%;
  padding: 5px 10px;
}

.title-modal{
  margin: 0 0 30px 0 ;
}

</style>
