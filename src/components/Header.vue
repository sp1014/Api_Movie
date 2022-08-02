
      <template>
  <div>
    <v-toolbar
      dark
      src="https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg">
      <v-toolbar-title>Movies</v-toolbar-title>
     
          <template v-slot:extension>
        <v-tabs align-with-title>
          <v-tab @click="ListBTN()">Home</v-tab>
          <v-tab @click="TransBTN()">New</v-tab>
      
        </v-tabs>
      </template>
      <v-spacer></v-spacer>
   
    
    </v-toolbar>
  </div>
</template>
<script>

export default {
  name: 'Header',


  methods:{
  
    ListBTN(){
   
      this.$router.push('/');
  
      
    },
      TransBTN(){
          this.$router.push('/nuevo');
      },
 
    
  }
}
</script>