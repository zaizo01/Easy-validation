<template>
  <div id="app">

   <div>
     {{ $data }}
   </div>
  
     <div>
        <p>Has trabajado con vue</p>
        <label for="">Si</label>
        <input type="radio" :value="true" v-model="form.exp">
        <label for="">No</label>
        <input type="radio" :value="false" v-model="form.exp">
     </div>

    <div v-if="form.exp">
      <p>Cuantos anos de experiencias tienes</p>
      <input type="text" v-model="form.years">
    
      <div v-if="form.years < 2">
        <p :style="styleInfo">Que te motivo a aprender vue</p>
        <textarea cols="30" rows="5" v-model="form.description" :class="descriptionFieldClasses"></textarea>
        <p v-if="descriptionError" class="info">{{ descriptionError }}</p>
      </div>

     <div v-else>
        <p>Cuentanos tu experiencias</p>
        <textarea cols="30" rows="5" v-model="form.description"></textarea>
        <p v-if="descriptionError != ''" class="info">{{ descriptionError }}</p>
     </div>

    </div>

   </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      form: {
        exp: null,
        years: null,
        description: ''

      }
    }
  },
  computed: {
    descriptionError(){
      let val = this.form.description.trim();

      if (val == ''){
        return 'El campo es obligatorio';
      }

      if(val.length < 5){
        return 'El campo debe de tener mas de 5 caracteres';
      }

      if(val.length > 20){
        return 'El campo debe de tener menos de 20 caracteres';
      }
      return;
    },
    descriptionFieldClasses(){
      return this.descriptionError ? 'info' : '';
    },
    styleInfo(){
      if (this.descriptionError) {
        return {color: 'red'}
      }
      return {color: 'green'}
    }

  },
}
</script>

<style lang="scss">
.info {
  color: red;
  border-color: red;
}
</style>
