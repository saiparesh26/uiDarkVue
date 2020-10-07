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
                            <a @click="onShow"> <i :id = "uuidMainIcon" ref="mainIcon" class="fas fa-plus"></i> </a>
                        </div>
                    </div>
                </div>
                
            </div>
            <div class="message-body" v-if="open">            
                <div class="level">
                    <div class="level-left">
                        <div class="level-item has-text-white">
                            File Type Generated 
                        </div>
                    </div>
                    <div class="level-right">
                        <div class="level-item">
                            <a> <i :id = 'uuidFileIcon' ref="fileIcon" class="fas fa-plus has-text-white" @click="showFileType"></i> </a>
                        </div>
                    </div>
                </div>
                <div v-if="showFile">
                    <div v-for="fileType in fileTypes" :key='fileType["File Type"]'>
                        <p class="has-text-white"> {{fileType["File Type"]}} </p>
                        <hr class="hr">
                    </div>
                </div>
                <hr class="hr"> 
                <div class="level">
                    <div class="level-left">
                        <div class="level-item has-text-white">
                            Pipelines Direct Linked 
                        </div>
                    </div>
                    <div class="level-right">
                        <div class="level-item">
                            <a> <i :id = 'uuidRegionIcon' ref="regionIcon" class="fas fa-plus has-text-white" @click="showRegions"></i> </a>
                        </div>
                    </div>
                </div>
                <div v-if="showRegion">
                    <div v-for="region in regions" :key='region["Region ID"]'>
                        <p class="has-text-white subtitle font-12"> Region : {{ region["Region ID"] }} </p>
                        <p class="has-text-white subtitle font"> {{ region.Pipeline }} </p>
                        <p class="has-text-white subtitle font"> {{ region.Region }} </p>
                        <hr class="hr">
                    </div>
                </div>
                <hr class="hr">
                <div class="level">
                    <div class="level-left">
                        <div class="level-item has-text-white">
                            Notebook 
                        </div>
                    </div>
                    <div class="level-right">
                        <div class="level-item">
                            <a> <i :id = 'uuidNoteBookIcon' ref="noteBookIcon" class="fas fa-plus has-text-white" @click="showNotebooks"></i> </a>
                        </div>
                    </div>
                </div>
                <div v-if="showNotebook">
                    <div v-for="notebook in notebooks" :key='notebook'>
                        <p class="has-text-white subtitle font-12"> {{ notebook['Notebook Path'] }} </p>
                        <hr class="hr">
                    </div>
                </div>
                <hr class="hr">
                <div class="level">
                    <div class="level-left">
                        <div class="level-item has-text-white">
                            Attributes({{ attributes.length }}) <span class="ml-2 mt-2"> <button class="button is-small is-rounded is-warning" @click="showModalData">  Show All </button> </span>
                        </div>
                    </div>
                    <div class="level-right">
                        <div class="level-item">
                            <a> <i :id = 'uuidAttributeIcon' ref="attributeIcon" class="fas fa-plus has-text-white" @click="showAttributes"></i> </a>
                        </div>
                    </div>
                </div>
                <div v-if="showAttribute">
                    <div v-for="attribute in attributes.slice(0,5)" :key='attribute'>                        
                        <p class="has-text-white subtitle font-12"> Name :  {{ attribute.target_object_attribute_name }} </p>
                        <hr class="hr">
                    </div>
                </div>
                <div class="modal" ref="modal">
                    <div class="modal-background"></div>
                    <div class="modal-card">
                        <header class="modal-card-head">
                        <p class="modal-card-title"> Attributes </p>
                        <button class="delete" aria-label="close" @click="closeModal"></button>
                        </header>
                        <section class="modal-card-body">
                        <!-- Content ... -->
                        
                        </section>
                        <footer class="modal-card-foot">                            
                        </footer>
                    </div>
                </div>
                <hr class="hr">                           
            </div>
        </article>   
    </div>
</template>

<script>
import axios from 'axios';
import { uuid } from 'vue-uuid';
export default {
    data: function(){
        return {
            showFile: false,
            open: false,
            fileTypes: [],
            regions: [],
            showRegion: false,
            showNotebook: false,
            notebooks:[],
            showAttribute: true,
            attributes: [],
            attributeCount: 0,
            loading: true,
            showModal: false,
            uuidMainIcon: uuid.v1(),
            uuidFileIcon: uuid.v1(),
            uuidRegionIcon: uuid.v1(),
            uuidNoteBookIcon: uuid.v1(),
            uuidAttributeIcon: uuid.v1()
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
        onShow: function(){
            this.open = !this.open;
            let mainIcon = this.$refs.mainIcon;
            if(!this.open){
                mainIcon.classList.remove('fa-mius');
                mainIcon.classList.add('fa-plus');
            }
            if(this.open){
                mainIcon.classList.add('fa-minus');
                mainIcon.classList.remove('fa-plus');
            }
            this.showAttributes();
            console.log(this.showModal);
        },
        showFileType: function(){
            this.showFile = !this.showFile;
            let fileIcon = this.$refs.fileIcon;
            if(!this.showFile){
                fileIcon.classList.remove('fa-minus');
                fileIcon.classList.add('fa-plus');
            }
            if(this.showFile){
                fileIcon.classList.add('fa-minus');
                fileIcon.classList.remove('fa-plus');
            }
            axios.get(`http://10.100.252.137:25009/getfiletype/${this.search}`)
             .then(res => {
                 this.fileTypes = JSON.parse(res.data);
                //  console.log(JSON.parse(res.data));
             })
             .catch(err => {
                 console.log(err);
             })
            
        },
        showRegions: function(){
            this.showRegion = !this.showRegion;
            // let regionIcon = document.getElementById('uuidRegionIcon');
            let regionIcon = this.$refs.regionIcon;
            if(!this.showRegion){
                regionIcon.classList.remove('fa-minus');
                regionIcon.classList.add('fa-plus');
            }
            if(this.showRegion){
                regionIcon.classList.add('fa-minus');
                regionIcon.classList.remove('fa-plus');
            }
            axios.get(`http://10.100.252.137:25009/getpipelinesregion/${this.search}`)
             .then(res => {
                 this.regions = JSON.parse(res.data);
                //  console.log(JSON.parse(res.data));
             })
             .catch(err => {
                 console.log(err);
             })
        },
        showNotebooks: function(){
            this.showNotebook = !this.showNotebook;
            // let noteBookIcon = document.getElementById('uuidNoteBookIcon');
            let noteBookIcon = this.$refs.noteBookIcon;
            if(this.showNotebook){
                noteBookIcon.classList.add('fa-minus');
                noteBookIcon.classList.remove('fa-plus');
            }
            if(!this.showNotebook){
                noteBookIcon.classList.remove('fa-minus');
                noteBookIcon.classList.add('fa-plus');
            }
            axios.get(`http://10.100.252.137:25009/getnotebookpath/${this.search}`)
             .then(res => {
                 this.notebooks = JSON.parse(res.data);
                //  console.log(this.notebooks);
             })
             .catch(err => {
                 console.log(err);
             })
        },
        showAttributes: function(){
            this.showAttribute = !this.showAttribute;
            let attributeIcon = this.$refs.attributeIcon;
            axios.get(`http://10.100.252.137:25009/getattributes/${this.search}`)
             .then(res => {
                 this.attributes = JSON.parse(res.data);
                //  console.log(this.attributes);
             })
             .catch(err => {
                 console.log(err);
             })

            if(this.showAttribute){
                attributeIcon.classList.add('fa-minus');
                attributeIcon.classList.remove('fa-plus');
            }
            if(!this.showAttribute){
                attributeIcon.classList.remove('fa-minus');
                attributeIcon.classList.add('fa-plus');
            }

            
        },
        showModalData: function(){
            // this.showModal = true;
            this.$refs.modal.classList.add('is-active');
        },
        closeModal: function(){
            this.$refs.modal.classList.remove('is-active');
        }
    }
}
</script>

<style scoped>
    .hr{
        height: 1px;
        background: white;
        opacity: 0.2;
    }
    /* .message{
        width: 350px;
    } */
    .message-body{
        background: #7F3CD2;
    }
    .message-header{
        background: #7F3CD2;
        display: block;
    }
    .font{
        font-size: 10px;
    }
    .font-12{
        font-size: 12px;
    }
</style>