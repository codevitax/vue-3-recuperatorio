<template>
    <div style="text-align: left">
        Lista de areas
       
        <table class="table">
            <thead>
                <tr>
                    <th scope="col">#</th>
                    <th scope="col">Area</th>
                    <th scope="col">Encargado</th>
                    <th scope="col">Numero de funcionarios</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(value, key) of personas" id="key">
                    <th scope="row">{{ value.id }}</th>
                    <td>{{ value.nombre }}</td>
                    <td>{{ value.direccion }}</td>
                    <td>
                        <button type="button" class="btn btn-primary" @click="editar(value)">Editar</button>
                        <button type="button" class="btn btn-danger" @click="eliminar(value)">Eliminar</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
        // import FormularioNuevaPersona from '@/components/FormularioNuevaPersona.vue'
        export default {
            name: 'PersonaView',
            props: [],
            emits: [],
            data(){
                return {
                    personas:[],
                    payload:{
                        nombre: "",
                        direccion: ""
                    }
                }
            },
            methods: {
                getPersonas(){
                    this.axios.get("http://localhost:5000/persona")
                    .then((response) => {this.personas = response.data})
                    .catch((err)=>{console.log(err);})
                },
                crearPersona(payload){
                    this.axios.post("http://localhost:5000/persona",payload)
                    .then((response) => {
                        //this.getPersonas(); console.log(response)
                        this.personas.push(response.data);
                    })
                    .catch((err)=>(console.log(err)))
                    console.log(this.payload);
                },
                editar(item){
                    this.$router.push('/persona/'+item.id+'/editar');
                    console.log(item)
                },
                eliminar(item){
                    this.axios.delete("http://localhost:5000/persona/"+item.id)
                    .then((response)=>{console.log(response);this.getPersonas();})
                    .catch((err)=>console.log(err))
                }
            },
            computed:{
            },
            mounted(){
                this.getPersonas();
            },
            components:{
                // FormularioNuevaPersona
            }
        }
</script>