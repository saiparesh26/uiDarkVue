<template>
  <div id="app" >
    <Topbar />
    <Navbar @searchItemClicked = 'getSearchField' />
    <BackToDashboard />
    <hr id="hr" class="mx-5">
    <!-- {{ searchField }} -->
    <div class="columns">
      <div class="column">
        <p class="title is-6 mb-5 has-text-centered" style="color: #5976D4">Universal Data Lake</p>
        <UniversalDatalake :source = 'udlResponse' :id = 'id' />
      </div>
      <div class="column">
        <p class="title is-6 mb-5 has-text-centered" style="color: #7F3CD2">Business Data Lake</p>
        <BDL :search = "bdlResponse" style="margin-bottom: 20px" />
        <L2 :l2Objects = "l2Objects" />
        <L3 :search = "searchField" />
        <BDLenhanced />
      </div>
      <div class="column">
        <p class="title is-6 mb-5 has-text-centered" style="color: #7F3CD2">Product Data Store</p>
      </div>
    </div>
  </div>
</template>

<script>
import 'bulma/css/bulma.css'
import Topbar from './components/Topbar.vue';
import UniversalDatalake from './components/UniversalDataLake.vue';
import BDL from './components/details.vue';
import L2 from './components/L2.vue';
import L3 from './components/L3.vue';
import BDLenhanced from './components/BDLEnhanced.vue';
import Navbar from './components/Navbar.vue';
import BackToDashboard from './components/BackDashboard.vue'
import axios from 'axios';

export default {
  name: 'App',
  data: function(){
      return {
        searchField: null,
        udlResponse: null,
        bdlResponse: null,
        id: null,
        l2Objects: null
      }
  },
  components: {
    Topbar,
    Navbar,
    UniversalDatalake,
    BDL,
    L2,
    L3,
    BDLenhanced,
    BackToDashboard
  },
  methods: {
    getSearchField: function(item){
      this.searchField = item;
      console.log(this.searchField);

      // Search field result
      axios.get(`http://10.100.252.137:25009/getobjectsources/${this.searchField}`)
       .then(res => {
         this.udlResponse = JSON.parse(res.data);
         this.bdlResponse = this.searchField;
        //  console.log(this.udlResponse);
       })
       .catch(err => {
         console.log(err);
       })
       
       // Object name found
       axios.get(`http://10.100.252.137:25009/objectnamefound/${this.searchField}`)
       .then(res => {
         this.id = JSON.parse(res.data);
         this.id = this.id[0].ID;
       })
       .catch(err => {
         console.log(err);
       })

       // L2 objects 
       axios.get(`http://10.100.252.137:25009/getl2objects/${this.searchField}`)
       .then(res => {
         this.l2Objects = JSON.parse(res.data);
         console.log(this.l2Objects); 
       })
       .catch(err => {
         console.log(err);
       })
    }
  }
}
</script>

<style scoped>
#app{
  min-height: 1024px;
  background: #0F212C;
}
#hr{
  margin-bottom: 100px;
  border: 0;
  height: 1px;
  background: white;
  opacity: 0.3;
}
</style>
