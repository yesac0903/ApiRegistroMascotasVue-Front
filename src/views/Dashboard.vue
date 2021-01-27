<template>
    <div>
        <Header/>

            <div class="container izquierda">

                <button class="btn btn-primary" v-on:click="nuevo()" >Nueva mascota</button>
                <br><br>


                <table class="table table-hover">
                <thead>
                    <tr>
                        <th scope="col">ID</th>
                        <th scope="col">Nombre</th>
                        <th scope="col">tags</th>
                        <th scope="col">Categoria</th>
                        <th scope="col">Status</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="mascota in Listamascotas" :key="mascota.idPet" v-on:click="editar(mascota.idPet)">
                        <th scope="row">{{ mascota.idPet}}</th>
                        <td>{{ mascota.namePet }}</td>
                        <td>{{ mascota.tags }}</td>
                        <td>{{ mascota.categoryPet }}</td>
                        <td>{{ mascota.status }}</td>
                    </tr>
            
                </tbody>
                </table>

            </div>

        <Footer />
    </div>
</template>
<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default {
    name:"Dashboard",
    data(){
        return {
            Listamascotas:null,
            pagina:1
        }
    },
    components:{
        Header,
        Footer
    },
    methods:{
            editar(id){
                this.$router.push('/editar/' + id);
            },
            nuevo(){
                this.$router.push('/nuevo');
            }
    },
    mounted:function(){
        let direccion = "http://localhost/registromascotas/mascotas?page=" + this.pagina;
        axios.get(direccion).then( data =>{
            this.Listamascotas = data.data;
        });
    }
}
</script>
<style  scoped>
    .izquierda{
        text-align: left;
    }
</style>