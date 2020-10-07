<template>
  <div id="app" >
    <Topbar />
    <Navbar @searchItemClicked = 'getSearchField' />
    <BackToDashboard :search = 'searchField' />
    <!-- <hr id="hr" class="mx-5"> -->
    <!-- {{ searchField }} -->
    <div class="columns">
      <div class="column">
        <p class="title is-6 mb-5 mt-5 has-text-centered" style="color: #5976D4">Universal Data Lake</p>
        <UniversalDatalake :source = 'udlResponse' :id = 'id' />
      </div>
      <div class="column">
        <p class="title is-6 mb-5 mt-5 has-text-centered" style="color: #7F3CD2">Business Data Lake</p>
        <BDL :search = "bdlResponse" style="margin-bottom: 50px; width: 400px" />
        <L2 :l2Objects = "l2Objects" />
        <L3 :l3Objects = "l3Objects" />
        <BDLenhanced :bdlenhancedObjects = "bdlenhancedObjects" />
      </div>
      <div class="column">
        <p class="title is-6 mb-5 mt-5 has-text-centered" style="color: #CF21FE">Product Data Store</p>
        <PDS :search = "bdlResponse" style="margin-bottom: 50px; width: 400px" />
      </div>
    </div>
  </div>
</template>

<script>
import 'bulma/css/bulma.css'
import Topbar from './components/Topbar.vue';
import UniversalDatalake from './components/UniversalDataLake.vue';
import BDL from './components/details2.vue';
import PDS from './components/details_pds.vue';
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
        l2Objects: null,
        l3Objects: null,
        bdlenhancedObjects: null
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
    BackToDashboard,
    PDS
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

       // L3 objects 
       axios.get(`http://10.100.252.137:25009/getl3objects/${this.searchField}`)
       .then(res => {
         this.l3Objects = JSON.parse(res.data);
         console.log(this.l3Objects); 
       })
       .catch(err => {
         console.log(err);
       })

       // BDL enhanced objects 
       axios.get(`http://10.100.252.137:25009/getbdlenhancedobjects/${this.searchField}`)
       .then(res => {
         this.bdlenhancedObjects = JSON.parse(res.data);
         console.log(this.bdlenhancedObjects); 
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

</style>
