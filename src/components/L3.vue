<template>
    <article class="message">
        <div class="message-header">
            <div class="level">
                <div class="level-left">
                    <div class="level-item">
                        <p class="subtitle is-6 has-text-white">Downstream Objects L3</p>
                    </div>
                </div>
                <div class="level-right" style="margin-left: 125px">
                    <div class="level-item">
                        <a @click="onShowL3"> <i id = "mainIconL3" class="fas fa-plus"></i> </a>
                    </div>
                </div>
            </div>
            
        </div>
        <div class="message-body" v-if="openL3">
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
            openL3: false
        }
    },
    methods: {
        onShowL3: function(){
            this.openL3 = !this.openL3;
            let mainIconL3 = document.getElementById('mainIconL3');
            if(!this.openL3){
                mainIconL3.classList.remove('fa-mius');
                mainIconL3.classList.add('fa-plus');
            }
            if(this.openL3){
                mainIconL3.classList.add('fa-minus');
                mainIconL3.classList.remove('fa-plus');
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