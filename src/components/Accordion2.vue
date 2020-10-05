<template>
    <article class="message" v-if="search">
        <div class="message-header">
            <div class="level">
                <div class="level-left">
                    <div class="level-item">
                        <p class="subtitle is-6 has-text-white"> {{search}} </p>
                    </div>
                </div>
                <div class="level-right">
                    <div class="level-item" >
                        <a @click="onShow"> <i id = "mainIcon" class="fas fa-plus"></i> </a>
                    </div>
                </div>
            </div>
            
        </div>
        <div class="message-body" v-if="open">
             
            <Detail value = 'File Type Generated' />
            <Detail value = 'Pipelines Direct linked' />
            <Detail value = 'Notebook' />
            <Detail value = 'Attributes(5)' />
            
            
        </div>
</article>
</template>

<script>
import 'bulma/css/bulma.css'
import Detail from './details.vue';
export default {
    props: {
        search: {
            type: String
        }
    },
    components: {
        Detail
    },
    data: function(){
        return {
            open: false
        }
    },
    methods: {
        onShow: function(){
            this.open = !this.open;
            let mainIcon = document.getElementById('mainIcon');
            if(!this.open){
                mainIcon.classList.remove('fa-mius');
                mainIcon.classList.add('fa-plus');
            }
            if(this.open){
                mainIcon.classList.add('fa-minus');
                mainIcon.classList.remove('fa-plus');
            }
        },
        onFileType: function(){
            // console.log('file type clicked');
        }
    }
}
</script>

<style scoped>
    .message{
        width: 350px;
    }
    .message-body{
        background: #7F3CD2;
    }
    .message-header{
        background: #7F3CD2;
        display: block;
    }
   
    
</style>