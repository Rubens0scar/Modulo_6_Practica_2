<template>
  <div>
    <menuMarket></menuMarket>
    <!-- <producto :idProducto="datos"></producto> -->
    <producto :productoP="{
        id: this.id,
        nombre: this.nombre,
        imagen: this.imagen,
        descripcion: this.descripcion,
        precio: this.precio,
        colores: this.colores
    }"></producto>
    <productoRel v-on:enlarge-text="onEnlargeText"></productoRel>
    <piePagina></piePagina>
  </div>
</template>

<script>
  import menuMarket from '@/components/menusMarket.vue'
  import piePagina from '@/components/pieMarket.vue'
  import producto from '@/components/productoMarket.vue'
  import productoRel from '@/components/productoRelacionadoMarket.vue'
  import axios from "axios";
  export default {
    name: 'principalMarket',
    data(){
      return {
        //datos: 1
        producto: [],
        id: 0,
        nombre: '',
        imagen: '',
        descripcion: '',
        precio: 0,
        colores: [],
      }
    },
    methods: {
      // onEnlargeText: function (enlargeAmount) {
      //   this.datos = enlargeAmount;
      // }
      onEnlargeText: async function (enlargeAmount) {
            try {
                const res = await axios.get(`http://localhost:3000/productos`, {
                    params: {
                        'id': enlargeAmount
                    },
                    headers:{
                        'content-type': 'application/json',
                        'accept': 'application/json'
                    }
                });
                this.producto = res.data;
                this.id = this.producto[0].id;
                this.nombre = this.producto[0].nombre;
                this.imagen = this.producto[0].imagen;
                this.descripcion = this.producto[0].descripcion;
                this.precio = this.producto[0].precio;
                this.colores = this.producto[0].colores;
            }catch(error){
                console.log(error);
            }
      }
    },
    computed: {
    },
    //mounted() {
    //},
    components: {
      menuMarket,
      piePagina,
      producto,
      productoRel
    },
  }
</script>

<style>
  .color-box {
        width: 40px;
        height: 40px;
        border-radius: 50%;
        margin: 7px;
        display: inline-block;
    }

    .clic{
        cursor: pointer;
    }

    .quantity button{
        border-radius: 50%;
        display: inline-block;
        width: 30px;
    }
    .quantity div{
        text-align: center;
        min-width: 30px;
        display: inline-block;
        font-weight: bold;
    }
    .buy-box{
        margin: 20px;
    }
    footer {
        
        text-align: center;
        padding: 30px 10px;
        margin-top: 50px;
        min-height: 100px;
    }
    .container{
        margin-top: 50px;
    }
    .producto-relacionado-precio{
        background: orangered;
        color: white;
        text-align: center;
        padding: 10px; 
    }
</style>
