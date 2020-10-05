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
                        <p class="has-text-white">Pipelines Direct linked</p>
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
            <div class="level">
                <div class="level-left">
                    <div class="level-item">
                        <p class="has-text-white">Attributes(5)</p>
                    </div>
                </div>
                <div class="level-right" >
                    <div class="level-item">
                        <a> <i class="fas fa-plus has-text-white"></i> </a>
                    </div>
                </div>
            </div>
            
        </div>
</article>
</template>

<script>
import 'bulma/css/bulma.css'
export default {
    props: {
        search: {
            type: String
        }
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