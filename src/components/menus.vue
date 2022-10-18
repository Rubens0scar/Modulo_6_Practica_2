<template>
    <div>
        <button @click="contador++">Hizo click {{contador}} veces.</button>
    </div>
</template>

<script>
    export default {
        name: 'contadorPropio',
        data(){
            return {
                contador: 0
            }
        },
        methods: {
        },
        computed: {
        },
        // mounted() {
        // },
        components: {
        },
    }
</script>

<style>

</style>