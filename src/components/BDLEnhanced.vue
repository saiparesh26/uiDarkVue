<template>
    <article class="message">
        <div class="message-header">
            <div class="level">
                <div class="level-left">
                    <div class="level-item">
                        <span class="tag" style="background: #28DA2E"> BDl Enhanced</span>
                    </div>
                </div>
                <div class="level-right" style="margin-left: 113px">
                    <div class="level-item">
                        <a @click="onShowBDL"> <i id = "mainIconBDL" class="fas fa-plus"></i> </a>
                    </div>
                </div>
            </div>
            
        </div>
        <div class="message-body" v-if="openBDL">
             <div class="level">
                <div class="level-left">
                    <div class="level-item">
                        <p class="has-text-white">File Type Generated</p>
                    </div>
                </div>
                <div class="level-right" >
                    <div class="level-item">
                        <a> <i class="fas fa-plus has-text-white"></i> </a>
                    </div>
                </div>
            </div>
            <hr class="hr">
            <div class="level">
                <div class="level-left">
                    <div class="level-item">
                        <p class="has-text-white">Notebook</p>
                    </div>
                </div>
                <div class="level-right" >
                    <div class="level-item">
                        <a> <i class="fas fa-plus has-text-white"></i> </a>
                    </div>
                </div>
            </div>
            <hr class="hr">

        </div>
</article>
</template>

<script>
import 'bulma/css/bulma.css'
export default {
    data: function(){
        return {
            openBDL: false
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
        width: 350px;
    }
    .message-body{
        background: #7F3CD2;
    }
    .message-header{
        background: #7F3CD2;
        display: block;
    }
    .hr{
        height: 1px;
        background: white;
        opacity: 0.2;
    }
</style>