<template>
  <div class="container">
    <h1>Random Gif Cat</h1>
    <form @submit.prevent="buscarGato">
      <div>
        <label for="titulo">Título: </label>
        <input type="titulo" class='form-control' v-model="titulo">
      </div>
      <br>
      <div>
        <label>Filtro: </label>
        <select class="custom-select" v-model="filtro">
          <option>blur</option>
          <option>mono</option>
          <option>sepia</option>
          <option>negative</option>
          <option>paint</option>
          <option>pixel</option>
        </select>
      </div>
      <br>
       <div>
        <label>Color: </label> 
        <select class="custom-select" v-model="color">
          <option value="red">rojo</option>
          <option value="blue">azul</option>
          <option value="green">verde</option>
          <option value="orange">naranjo</option>
          <option value="yellow">amarillo</option>
        </select>
         <span class="color" :style="{backgroundColor: this.color}"></span>
      </div>
      <br>
      <div>
        <label for="size">Tamaño: </label>
        <input type="size" class="form-control" v-model="size">
      </div>
      <br>
      <button type="submit" class="btn btn-primary" v-on:click="validar">Obtener gatito</button>
    </form>
    <section class="resultado">
      <img :src="imagen" alt="">
    </section>
  </div>
</template>

<script>
export default {
  name: 'Gifcat',
  data() {
    return {
      titulo: '',
      filtro: '',
      color: '',
      size: '',
      imagen: '',
    }
  },
  methods: {
    validar() {
      if (this.titulo === '') {
        alert('Escriba un título');
        return false;
      }
      else if (this.filtro === '') {
        alert('FElija un filtro');
        return false;
      }
      else if (this.color === '') {
        alert('Elija color');
        return false;
      }
      else if (this.size === '') {
        alert('Ingrese tamaño en pixeles');
        return false;
      }
      else if (isNaN(this.size)) {
        alert('Solo acepta valores numéricos');
        return false;
      }
    },
    buscarGato(){
      fetch(`https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.size}`)
      .then(result => {
        console.log(result);
        this.imagen = result.url;
      });
    },
  }
}
</script>


<style>
body, html{
  margin: 0px !important;
}
h1 {
  text-align: center;
  padding-top: 80px;
  padding-bottom: 40px;
  margin: 0px;  
}
form {
  padding-top: 20px;
  padding-bottom: 20px;
  text-align: center;
  display: block;
}
.resultado {
  text-align: center;
  padding-top: 20px;
  padding-bottom: 300px;
  margin: 0px;
}
.color {
  width: 30px;
  height: 30px;
  background-color: white;
  display: inline-block;
  margin-top: 20px;
}
</style>