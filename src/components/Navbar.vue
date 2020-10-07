<template>
    <section id="navbar">
       
        <div class="columns">
            <div class="column">
                <p class="title has-text-white ml-5 mt-5">Data Lineage Platform</p>
                <p class="subtitle has-text-white ml-5 mb-5">What this screen supposed to do</p>
            </div>
            <div class="column">
                <div class="field mr-5 mt-5" id="searchDiv">
                    <p class="control has-icons-left">
                      <input class="input is-small is-rounded has-text-centered mt-3 mr-3" type="text" placeholder="Search" v-model="item" @input="onChange" @focus="modal = true">
                      <span class="icon is-small is-left mt-3">
                        <i class="fas fa-search"></i>
                      </span>
                      
                    </p>
                  </div> 
                  <div v-if="items && modal" >
                    <ul id = "ul" class="is-rounded">
                        <li id="li" class="has-background-light has-text-black py-2 px-3" v-for="item in items" :key="item.object_name" @click="setItem(item)"> {{item.object_name}} </li>
                    </ul>
                </div>                  
            </div>
        </div>  
    </section>
</template>

<script>
import axios from 'axios';
export default {
    name: "Navbar",
    data : function(){
        return {
            item: '',
            modal:false,
            items:[],
            filteredItems:[]
        }
    },
    
    methods: {
        onChange: function(){
            if(this.item.length <= 3){
                var ul = document.getElementById('ul');
                this.items = [];
                ul.innerHTML = '';
            }
            else if(this.item.length > 3){
                axios.get(`http://10.100.252.137:25009/objectnamesearch/${this.item}`)
                 .then(res => {
                     this.items = JSON.parse(res.data);
                     console.log(this.items);
                 })
                 .catch(err => {
                     console.log(err)
                 })
            }
            
        },
        setItem: function(item){
            this.item = item.object_name;
            this.modal = false;
            this.$emit('searchItemClicked', item.object_name);  // Send data to parent
        }
    }
}
</script>

<style scoped>
    #navbar{
        background: linear-gradient(90deg, #421C79 0%, #A06EC0 100%), #C4C4C4;
    }

    #searchDiv{
        width: 300px; 
        margin-left: 300px;
    }

    #ul{
        width: 300px;
        height: 200px;
        overflow: auto;
        margin-left: 300px;
    }
    #li{
        border-bottom: 1px solid black;
        height: 50px;
        cursor: pointer;
    }
</style>