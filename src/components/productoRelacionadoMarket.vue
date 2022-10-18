<template>
    <div class="container ">

        <div class="row">
            <h4>Productos relacionados</h4>
        </div>
        <div class="row">
            <template v-for="productosRel of prodRel" :key="productosRel.id">
                <div class="col">
                    <div class="card" style="width: 18rem;cursor:pointer;" v-on:click="seleccionado(productosRel.id)">
                        <div class="card-body">
                            <h5 class="card-title">{{productosRel.nombre}}</h5>
                            <img :src="productosRel.imagen" alt="" :style="`width:${tamanio}`">
                            <p class="card-text">{{productosRel.descripcion}}.</p>
                            <div class="producto-relacionado-precio" v-bind:style="precioEstilos">Precio: {{idProductoRel}}
                                {{productosRel.precio}} BOB</div>
                            <div>
                                <div>
                                    <div class="color-box" v-for="color in productosRel.colores" :key="color.id" :style="`background: ${color}`"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </template>
        </div>
    </div>
</template>

<script>
    import axios from "axios";
    export default {
        props: {
            idProductoRel: {
                type: Number,
                default: 1
            }
        },
        name: 'productosRelacionados',
        data(){
            return {
                productos: [2,3,4],
                prodRel: [],
                tamanio: '100%',
                idProdRel: this.idProductoRel,
            }
        },
        async created(){
            const res = await axios.get(`http://localhost:3000/productos`, {
                    params: {
                        'id': this.productos
                    },
                    headers:{
                        'content-type': 'application/json',
                        'accept': 'application/json'
                    }
            });
            this.prodRel = res.data;
        },
        methods: {
            seleccionado: async function(id){
                this.productos.push(Number(this.idProdRel));
                this.productos=this.productos.filter(function(item){
                    return item !== id
                });
                this.idProdRel = id;
                const res = await axios.get(`http://localhost:3000/productos`, {
                        params: {
                            'id': this.productos
                        },
                        headers:{
                            'content-type': 'application/json',
                            'accept': 'application/json'
                        }
                });
                this.prodRel = res.data;
                
                
                //this.$emit('idProducto',{Number: 2});

                this.$emit('enlarge-text', id);

            },
        },
        computed: {
        },
        //mounted() {
        //},
        components: {
        },
    }
</script>

<style>

</style>