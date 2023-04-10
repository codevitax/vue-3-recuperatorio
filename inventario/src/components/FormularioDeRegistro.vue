<template>
    <div style="text-align: left">
        <form @submit.prevent="$event => crearPersona()">
            <input type="text" v-model="payload.nombre" placeholder="Nombre">
            <input type="text" v-model="payload.direccion" placeholder="Direccion">
            <button type="submit">Agregar</button>
        </form>
    </div>
</template>

<script>
        export default {
            name: 'FormularioNuevaPersona',
            props: ["inpayload"],
            emits: ["on-payload"],
            data(){
                return {
                    payload: {
                        nombre:"",
                        direccion:""
                    }
                }
            },
            methods: {
                crearPersona(){
                    this.$emit('on-payload',this.payload);
                }
            },
            computed:{
            },
            mounted(){
                this.payload = this.inpayload;
            },
            components:{
            }
        }
</script>