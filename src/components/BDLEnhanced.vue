<template>
    <article class="message" v-if="bdlenhancedObjects.length > 0">
        <div class="message-header">
            <div class="level">
                <div class="level-left">
                    <div class="level-item">
                        <span class="tag" style="height:30px; background:#28DA2E"> BDL Enhanced </span>
                    </div>
                </div>
                <div class="level-right">
                    <div class="level-item">
                        <a @click="onShowBDL"> <i id = "mainIconBDL" class="fas fa-plus"></i> </a>
                    </div>
                </div>
            </div>
            
        </div>
        <div class="message-body" v-if="openBDL">
             
            
                <div v-for="bdlenhancedObject in bdlenhancedObjects" :key="bdlenhancedObject.ID">
                    <!-- <p class="has-text-white subtitle is-6"> Name : {{ l2Object.Name }}</p> -->
                    <Detail :search = 'bdlenhancedObject.Name' />
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
        bdlenhancedObjects: {
            type: Array
        }
    },
    components: {
        Detail
    },
    data: function(){
        return {
            openBDL: false,
            bdlNames: []
        }
    },
    methods: {
        onShowBDL: function(){
            this.openBDL = !this.openBDL;
            let mainIconBDL = document.getElementById('mainIconBDL');
            if(!this.openBDL){
                mainIconBDL.classList.remove('fa-mius');
                mainIconBDL.classList.add('fa-plus');
            }
            if(this.openBDL){
                mainIconBDL.classList.add('fa-minus');
                mainIconBDL.classList.remove('fa-plus');
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