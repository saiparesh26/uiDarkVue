<template>
    <article class="message" v-if="l2Objects.length > 0">
        <div class="message-header">
            <div class="level">
                <div class="level-left">
                    <div class="level-item">
                        <span class="tag is-primary" style="border-radius: 50%; height:30px; background:#FE7E4C"> L2</span>
                    </div>
                </div>
                <div class="level-right">
                    <div class="level-item">
                        <a @click="onShowL2"> <i id = "mainIconL2" class="fas fa-plus"></i> </a>
                    </div>
                </div>
            </div>
            
        </div>
        <div class="message-body" v-if="openL2">
             
            
                <div v-for="l2Object in l2Objects" :key="l2Object.ID">
                    <!-- <p class="has-text-white subtitle is-6"> Name : {{ l2Object.Name }}</p> -->
                    <Detail :search = 'l2Object.Name' />
                    <hr class="hr">
                </div>
            
        </div>
</article>
</template>

<script>
import 'bulma/css/bulma.css'
import Detail from './details2.vue';
export default {
    props: {
        l2Objects: {
            type: Array
        }
    },
    components: {
        Detail
    },
    data: function(){
        return {
            openL2: false,
            l2Names: []
        }
    },
    methods: {
        onShowL2: function(){
            this.openL2 = !this.openL2;
            let mainIconL2 = document.getElementById('mainIconL2');
            if(!this.openL2){
                mainIconL2.classList.remove('fa-mius');
                mainIconL2.classList.add('fa-plus');
            }
            if(this.openL2){
                mainIconL2.classList.add('fa-minus');
                mainIconL2.classList.remove('fa-plus');
            }
        
            
        }
    }
}
</script>

<style scoped>
    .message{
        width: 400px;
    }
    .message-body{
        background: #ab6ff5;
    }
    .message-header{
        background: #ab6ff5;
        display: block;

    }
    .hr{
        height: 1px;
        background: white;
        opacity: 0.2;
    }
</style>