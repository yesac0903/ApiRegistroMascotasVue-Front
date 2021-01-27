<template>
     <div>
          <Header />
            <div class="container">
                <form action="" class="form-horizontal">
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">Nombre</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="nombre" id="namePet" v-model="form.namePet">
                       </div>
                    </div>
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">Tags</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="tags" id="tags" v-model="form.tags">
                       </div>
                    </div>
                    <div class="form-group left row">
                      <div class="col">
                            <label for="" class="control-label col-sm-3">Categoria</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="categoria" id="categoryPet" v-model="form.categoryPet">
                            </div>
                        </div>
                        <div class="col">
                          <label for="" class="control-label col-sm-5">status</label>
                          <div class="col-sm-7">
                              <input type="text" class="form-control" name="status" id="status" v-model="form.status">
                          </div>
                        </div> 
                    </div>
                    

                    <div class="form-group">
                      <button type="button" class="btn btn-primary" v-on:click="guardar()" >Guardar</button>
                      <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                    </div> 
                </form>


            </div>
        <!-- <Footer /> -->

    </div>
</template>
<script>
import Header from '@/components/Header.vue'
//import Footer from '@/components/Footer.vue'
import axios from 'axios';
export default {
    name:"Nuevo",
    data:function(){
        return {
            form:{
                "namePet" :"",
                "categoryPet" :"",
                "status":"",
                "tags": "", 
                "token" : "" 
            }
        }
    },
    components:{
        Header,
        //Footer
    },
    methods:{
        guardar(){
            this.form.token = localStorage.getItem("token");
            axios.post("http://localhost/registromascotas/mascotas",this.form)
            .then(data =>{
                console.log(data);
                this.makeToast("Has agregado una nueva mascota","success");
                this.$router.push("/dashboard");
            }).catch( e =>{
                console.log(e);
                 this.makeToast("Error","Error al guardar","error");
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        makeToast(titulo,texto,tipo) {
            this.toastCount++
            this.$bvToast.toast(texto, {
            title: titulo,
            variant: tipo,
            autoHideDelay: 5000,
            appendToast: true
            })
        }
        
    }
}
</script>
<style scoped>
.left{
    text-align:  left;
}
</style>