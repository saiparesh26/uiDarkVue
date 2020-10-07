<template>
    <article class="message" v-if="pdsRolePlayObjects.length > 0">
        <div class="message-header">
            <div class="level">
                <div class="level-left">
                    <div class="level-item">
                        <span class="tag" style=" height:30px; background:#28DA2E"> PDSRolePlay</span>
                    </div>
                </div>
                <div class="level-right">
                    <div class="level-item">
                        <a @click="onShowPDSRolePlay"> <i id = "mainIconPDSRolePlay" class="fas fa-plus"></i> </a>
                    </div>
                </div>
            </div>
            
        </div>
        <div class="message-body" v-if="openPDSRolePlay">
             
            
                <div v-for="pdsRolePlayObject in pdsRolePlayObjects" :key="pdsRolePlayObject.ID">
                    <!-- <p class="has-text-white subtitle is-6"> Name : {{ PDSRolePlayObject.Name }}</p> -->
                    <Detail :search = 'pdsRolePlayObject.Name' />
                    <hr class="hr">
                </div>
            
        </div>
</article>
</template>

<script>
import 'bulma/css/bulma.css'
import Detail from './roleplayDetails.vue';
export default {
    props: {
        pdsRolePlayObjects: {
            type: Array
        }
    },
    components: {
        Detail
    },
    data: function(){
        return {
            openPDSRolePlay: false,
            PDSRolePlayNames: []
        }
    },
    methods: {
        onShowPDSRolePlay: function(){
            this.openPDSRolePlay = !this.openPDSRolePlay;
            let mainIconPDSRolePlay = document.getElementById('mainIconPDSRolePlay');
            if(!this.openPDSRolePlay){
                mainIconPDSRolePlay.classList.remove('fa-mius');
                mainIconPDSRolePlay.classList.add('fa-plus');
            }
            if(this.openPDSRolePlay){
                mainIconPDSRolePlay.classList.add('fa-minus');
                mainIconPDSRolePlay.classList.remove('fa-plus');
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
        background: #ac46c9;
    }
    .message-header{
        background: #ac46c9;
        display: block;

    }
    .hr{
        height: 1px;
        background: white;
        opacity: 0.2;
    }
</style>