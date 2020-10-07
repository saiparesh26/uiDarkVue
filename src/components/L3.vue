<template>
    <article class="message" v-if="l3Objects.length > 0">
        <div class="message-header">
            <div class="level">
                <div class="level-left">
                    <div class="level-item">
                        <span class="tag" style="height:30px; background:#EF3B43"> L3</span>
                    </div>
                </div>
                <div class="level-right">
                    <div class="level-item">
                        <a @click="onShowL3"> <i id = "mainIconL3" class="fas fa-plus"></i> </a>
                    </div>
                </div>
            </div>
            
        </div>
        <div class="message-body" v-if="openL3">
             
            
                <div v-for="l3Object in l3Objects" :key="l3Object.ID">
                    <!-- <p class="has-text-white subtitle is-6"> Name : {{ l3Object.Name }}</p> -->
                    <Detail :search = 'l3Object.Name' />
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
        l3Objects: {
            type: Array
        }
    },
    components: {
        Detail
    },
    data: function(){
        return {
            openL3: false,
            l3Names: []
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
            // for(let i = 0 ; i< l2Objects.length; i++){
            //     this.l2Names[i] = this.l2Objects[i].Name;
            //     console.log(this.l2Names[i]);
            // }
            
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