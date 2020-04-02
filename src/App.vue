<template>
  <div id="app">

    <div class="row">
      <div class="col-md-7">
        <div class="row">
          <div class="col-md-6" v-for="prod in productos" :key="prod.id">
            <!--Se llama :producto a la función que va a cumplir el archivo Producto.vue mediante props-->
            <producto :producto="prod" v-on:agregar-carro="agregarProdCarro" :estaEnCarrito="estaEnCarrito(prod)"></producto>
          </div>
        </div>
      </div>

      <!--Producto le manda al padre App y App le manda a carrito-->
      <div class="col-md5 my-5">
        <carrito :items="carrito" v-on:pagar="pagar" v-on:remover-item="removerProducto"></carrito>
      </div>
    </div>

  </div>
</template>

<script>

import productos from './productos.json'
import Producto from './components/Producto.vue'
import Carrito from './components/Carrito.vue'

export default {
  name: 'app',
  components: {
    Producto,
    Carrito        
  },
  data(){
    return {
      productos,
      carrito:[]
    }
  },
  methods:{
    agregarProdCarro(producto){
      //Carrito es un arreglo de productos
      this.carrito.push(producto);
    },
    estaEnCarrito(producto){
      const item = this.carrito.find(item => item.id === producto.id);
      if(item){
        return true;
      }
      return false;
    },
    //filter elimina el producto del carrito
    removerProducto(producto){
      this.carrito = this.carrito.filter(item => item.id != producto.id);
    },
    pagar(){
      this.carrito = [];
      alert('Venta completada !!!');
    }
  }
}
</script>

<style>

</style>
