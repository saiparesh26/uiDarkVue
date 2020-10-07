<template>
    <div id="div">
        <article class="message" v-if="search">
            <div class="message-header">
                <div class="level">
                    <div class="level-left">
                        <div class="level-item">
                            <p class="subtitle is-6 has-text-white"> {{search}}                                 
                                <span v-if="badge === 'L2'" class="tag" style="border-radius: 50%; height:30px; background:#FE7E4C; margin-left: 10px"> {{badge}} </span>
                                <span v-if="badge === 'L3'" class="tag" style="border-radius: 50%; height:30px; background:#EF3B43; margin-left: 10px"> {{badge}} </span>  
                            </p>
                        </div>
                    </div>
                    <div class="level-right">
                        <div class="level-item" >
                            <a @click="showModalData"> <i  class="fas fa-plus"></i> </a>
                        </div>
                    </div>
                </div>
                
            </div>
            <div class="modal" ref="modal">
                <div class="modal-background"></div>
                    <div class="modal-card">
                        <header class="modal-card-head" style="background: #8e21ac">
                            <p class="modal-card-title has-text-white"> {{search}} </p>
                            <button class="delete" aria-label="close" @click="closeModal"></button>
                        </header>
                        <section class="modal-card-body">
                        <!-- Content ... -->
                        <!-- File types -->
                        <!-- <div>
                            <p class="title is-5">File Types Generated</p>  
                                <div class="content">                          
                                    <ul>
                                        <li class="list" v-for="fileType in fileTypes" :key='fileType["File Type"]'> <p class="font-14"> {{fileType["File Type"]}} </p> </li>
                                    </ul>
                                </div>                            
                            <hr class="hr">
                        </div> -->

                        <!-- Pipelines -->
                        <!-- <div>
                            <p class="title is-5">Pipelines Direct Linked</p>
                            <div class="content">  
                                <ul>
                                    <li v-for="region in regions" :key='region["Region ID"]'>
                                        <p class="subtitle font-14"> Region : {{ region.Region }} ( {{ region["Region ID"] }} ) </p>
                                        <p class="subtitle font-14"> {{ region.Pipeline }} </p>
                                       
                                        <hr class="hr2">
                                    </li>
                                </ul>
                            </div>  
                            <hr class="hr">                             
                        </div>     -->

                        <!-- Notebook -->
                        <!-- <div>
                            <p class="title is-5">Notebook</p>
                            <div class="content">
                                <ul>
                                    <li v-for="notebook in notebooks" :key='notebook'>
                                        <p class="subtitle font-14"> {{ notebook['Notebook Path'] }} </p>
                                    </li>
                                </ul> 
                            </div>  
                            <hr class="hr">                     
                        </div> -->

                        <!-- Attributes -->
                        <div>
                            <p class="title is-5">Attributes <span style = "margin-top: 10px; margin-left:10px"> <button class="button is-small is-rounded" style="background: #8e21ac" @click="showAllAttributesModal"> <span class="has-text-white"> Show All </span></button> </span> </p>
                            <div class="content">
                                <ul>
                                    <li v-for="attribute in attributes.slice(0,5)" :key='attribute'>
                                        <p class="subtitle font-14"> {{ attribute.target_object_attribute_name }} </p>
                                    </li>
                                </ul>  
                            </div>
                            <hr class="hr">                          
                        </div>
                        <div class="modal" ref="attributesModal">
                            <div class="modal-background"></div>
                                <div class="modal-card">
                                    <header class="modal-card-head" style="background: #8e21ac">
                                        <p class="modal-card-title has-text-white"> {{search}} - Attributes </p>
                                        <button class="delete" aria-label="close" @click="closeAttributesModal"></button>
                                    </header>
                                    <section class="modal-card-body">
                                    <!-- Content ... -->
                                    <div class="content">
                                        <ul>
                                            <li v-for="attribute in attributes" :key='attribute'>
                                                <p class="subtitle font-14"> {{ attribute.target_object_attribute_name }} </p>
                                            </li>
                                        </ul>
                                    </div>
                                    </section>
                                    
                                </div>
                        </div>
                        </section>
                        
                </div>
            </div>
        </article>   
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data: function(){
        return { 
            fileTypes: [],
            regions: [],                       
            notebooks:[],
            attributes: [],
        }
    },
    props: {
        search:{
            type: String
        },
        badge: {
            type: String
        }
    },
    
    methods: {
        
        showModalData: function(){
            this.$refs.modal.classList.add('is-active');

            // Fetching file types
            axios.get(`http://10.100.252.137:25009/getfiletype/${this.search}`)
                .then(res => {
                    this.fileTypes = JSON.parse(res.data);
                    //  console.log(JSON.parse(res.data));
                })
                .catch(err => {
                    console.log(err);
                })

            // Fetching pipelines
            axios.get(`http://10.100.252.137:25009/getpipelinesregion/${this.search}`)
                .then(res => {
                    this.regions = JSON.parse(res.data);
                    //  console.log(JSON.parse(res.data));
                })
                .catch(err => {
                    console.log(err);
                })

            // Fetching notebook
            axios.get(`http://10.100.252.137:25009/getnotebookpath/${this.search}`)
                .then(res => {
                    this.notebooks = JSON.parse(res.data);
                    //  console.log(this.notebooks);
                })
                .catch(err => {
                    console.log(err);
                })

            // Fetching attributes
            axios.get(`http://10.100.252.137:25009/getattributes/${this.search}`)
                .then(res => {
                    this.attributes = JSON.parse(res.data);
                    //  console.log(this.attributes);
                })
                .catch(err => {
                    console.log(err);
                })
        },
        closeModal: function(){
            this.$refs.modal.classList.remove('is-active');
        },
        showAllAttributesModal: function(){
            this.$refs.attributesModal.classList.add('is-active');
        },
        closeAttributesModal: function(){
            this.$refs.attributesModal.classList.remove('is-active');
        }
    }
}
</script>

<style scoped>
    .hr{
        height: 1px;
        background: grey;
        opacity: 0.2;
    }
    .hr2{
        height: 1px;
        background: grey;
        opacity: 0.2;
        margin-left: 20px;
        margin-right: 20px;
    }
    /* .message{
        width: 350px;
    } */
    .message-body{
        background: #8e21ac;
    }
    .message-header{
        background: #8e21ac;
        display: block;
    }
    .font{
        font-size: 10px;
    }
    .font-14{
        font-size: 14px;
    }
    /* .list{
        list-style-type: circle;
    } */
</style>