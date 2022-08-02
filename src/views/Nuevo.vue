<template>
    <div>
        <Header />
 <div class="container">
        <div class="row">
            <div class="col">               
                <div class="shadow-lg p-3 mb-5 mt-4 bg-body rounded">                                    
                    <div class="p-3 mb-2 bg-primary bg-gradient fw-bold text-white">Create movie</div>
                    <form class="row g-3 needs-validation" novalidate id="form" name="form" v-on:submit.prevent="procesar();" >
                         <div class="col-md-4 position-relative">
                            <label for="original_title" class="form-label">original_title</label>
                          <input type="text" class="form-control" name="original_title" id="original_title" v-model="form.original_title" required>
                        </div>
                        <div class="col-md-4 position-relative">
                            <label for="overview" class="form-label">overview</label>
                          <input type="text" class="form-control" name="overview" id="overview" v-model="form.overview" required>                  
                        </div>
                        <div class="col-md-4 position-relative">
                            <label for="release_date" class="form-label">release_date</label>
                               <input type="date" class="form-control" name="release_date" id="release_date" v-model="form.release_date" required>       
                       </div>                                             
                       
                            <div class="col-md-4 position-relative">
                            <label for="nombre" class="form-label">Image</label>        
                              <input class="form-control" type="file" id="formFile" multiple  v-on:change="getFile($event)" required /> 
                               {{form.Archivos}}                    
                        </div>              
                        <div class="col-12">
                          <button type="submit" class="btn btn-primary fw-bold float-end" v-on:click="guardar()" >Save</button>              
                         <button type="button" class="btn btn-dark margen fw-bold float-end" v-on:click="salir()"  >leave</button>
                      </div>
                    </form>
                </div>
            </div>
        </div>
    </div>        
    </div>
</template>
<script src="https://unpkg.com/sweetalert/dist/sweetalert.min.js"></script>
<script>
import Header from '@/components/Header.vue'
import axios from 'axios';
import swal from 'sweetalert';
import global from "../../config.js";
export default {
    data:function(){
        return {
            submited: false,
              file: "",
           form:{
              "original_title": "",
              "overview": "",
              "release_date":"",
              "Archivos": "",
               errors: []
          },
          uploadURL: global.URL_FILE,
        }
    },
    components:{
        Header
    },

    methods:{ 
           getFile(event) {
      var ValidationFile = document.getElementById("formFile").files[0].size;
      if (ValidationFile > 500000000) {
        alert("El archivo no debe pesar mas de 500MB");
      } else {
        this.file = event.target.files[0];
          this.form.Archivos = this.file.name 
      }
    },
        guardar(){       
             console.log(this.form);  
              this.$store.commit("getUser", this.form);
                swal({title: "Good job!",  text: "Ok",
                   icon: "success",
                   }) 
            this.$router.push("/");
        },
       procesar(){
            this.submited = true;
            this.$v.$touch();
            if(this.$v.$invalid){
                return false;
            }
        },       
       salir(){
            this.$router.push("/");
        },
        makeToast(titulo,texto,tipo) {
            this.toastCount++
            this.$bvToast.toast(texto, {
            title: titulo,
            variant: tipo,
            autoHideDelay: 5000,
            appendToast: true
            })
        },  

    }
}
</script>
<style scoped>
.left{
    text-align:  left;
}
</style>