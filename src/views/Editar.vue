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
                      <button type="button" class="btn btn-primary" v-on:click="editar()" >Editar</button>
                      <button type="button" class="btn btn-danger margen" v-on:click="eliminar()" >Eliminar</button>
                      <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                    </div> 
                </form>
            </div>
          <!-- <Footer />   -->
        </div>
    
</template>
<script>
import Header from '@/components/Header.vue';
//import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default {
  name:"Editar",
  components:{
    Header,
    //Footer
  },
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
  methods:{
      editar(){
          axios.put("http://localhost/registromascotas/mascotas",this.form)
          .then( data =>{
              console.log(data);
          })
      },
      salir(){
        this.$router.push("/dashboard");
      },
      eliminar(){
        var enviar = {
            "idPet" : this.form.idPet,
            "token" : this.form.token
        };
        axios.delete("http://localhost/registromascotas/mascotas", { headers : enviar})
        .then( datos => {
            console.log(datos);
           this.$router.push("/dashboard");
        });

      }
  },
  mounted:function(){
      this.form.idPet = this.$route.params.id;
      axios.get("http://localhost/registromascotas/mascotas?id="+ this.form.idPet)
      .then( datos => {
        
        this.form.namePet = datos.data[0].namePet;
        this.form.categoryPet = datos.data[0].categoryPet;
        this.form.status = datos.data[0].status;
        this.form.tags = datos.data[0].tags;
        this.form.token = localStorage.getItem("token");
        console.log(this.form);

      })
     
  }  
}
</script>
<style scoped>
 .left{
   text-align: left;
 };
 .margen{
   margin-left: 15px;
   margin-right: 15px;;
 }
</style>