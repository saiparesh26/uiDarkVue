<template>
    <div v-if="source && id"> 
        <article class="message">
            <div class="message-body">
                <div class="level">
                        <div class="level-item">
                            <p class="subtitle is-6 has-text-white">{{ source[0].Object}}</p>                            
                        </div>
                </div> 
                <div class="level">
                        <div class="level-item">
                            <p class="subtitle is-6 has-text-white"> {{ id }} </p>                            
                        </div>
                </div>            
            </div>
        </article>
    </div>
</template>

<script>
export default {
    name: 'udl',
    props: {
        source: {
            type: Array
        },
        id: {
            type: String
        }
    },
    data: function(){
        return {
            sourceitem: null
        }
    },
    
}
</script>

<style scoped>
    .message{
        width: 350px;
        background: #484AA7;
    }
    .message-body{
        background: #484AA7;
        border-left: 0;
    }
</style>