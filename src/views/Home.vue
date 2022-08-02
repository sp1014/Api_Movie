<template>
    <div>
      <Header />
           
            <div class="container izquierda">
               <button class="btn btn-primary" v-on:click="New()">New Movie</button>
               <br>
               
                <table class="table table-hover">
                <thead>
                    <tr>
                           <th scope="col">Image</th>
                        <th scope="col">ID</th>
                        <th scope="col">original_title</th>
                        <th scope="col">overview</th>
                        <th scope="col">release_date</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="dat in datos" :key="dat.id" >
                         <td><img :src="`https://image.tmdb.org/t/p/w185_and_h278_bestv2${dat.poster_path}`"></td>
                        <th scope="row">{{ dat.id}}</th>
                        <td>{{ dat.original_title }}</td>
                        <td>{{ dat.overview }}</td>
                        <td>{{ dat.release_date }}</td>
                    </tr>
                </tbody>
                </table>
            </div>
    </div>
</template>
<script>
import Header from '@/components/Header.vue'
import axios from 'axios';
import global from "../../config.js";
export default {
    name: "Dashboard",
       components:{
        Header
    },
    data(){
        return{
            datos:null,
            dato:''
        }
    },
    methods:{
     New(){
           this.$router.push('/nuevo');
     }
    },
    mounted:function(){
        let direccion = global.API_MOVIE;
        axios.get( direccion).then(data =>{

           this.datos=data.data.results;
           console.log(this.dato);
        })
    },
         computed:{
        data(){
            this.dato =  this.$store.state.data.form
          return this.$store.state.dato;
        }
      },
    
}
</script>

<style  scoped>
    .izquierda{
        text-align: left;
    }
</style>



