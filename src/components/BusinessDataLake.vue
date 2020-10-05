<template>

    <div class="dropdown" style="margin-left:50px" v-if="search">
        <div class="dropdown-trigger">
            <div class="p-3" aria-haspopup="true" aria-controls="dropdown-menu2">
                <span class="has-text-white">BillingDocumentLine</span>
                <a  class="icon is-small" style="margin-left: 100px" @click="dropdownToggle">
                    <i id="dropDownButton" class="fas fa-plus has-text-white" aria-hidden="true"></i>
                </a>
            </div>
        </div>
        <div class="dropdown-menu" id="dropdown-menu2" role="menu" style="width:100%">
            <div class="dropdown-content">
                <div class="dropdown-item">
                    <div class="level">
                        <div class="level-left">
                            <div class="level-item has-text-white">
                                File type Generated
                            </div>
                        </div>
                        <div class="level-right">
                            <div class="level-item">
                                <a> <i class="fas fa-plus has-text-white"></i> </a>
                            </div>
                        </div>
                    </div>
                </div>
                <hr class="dropdown-divider">

                <div class="dropdown-item">
                    <div class="level">
                        <div class="level-left">
                            <div class="level-item has-text-white">
                                Pipelines Direct Linked
                            </div>
                        </div>
                        <div class="level-right">
                            <div class="level-item">
                                <a> <i class="fas fa-plus has-text-white"></i> </a>
                            </div>
                        </div>
                    </div>
                </div>
                <hr class="dropdown-divider">
                
                <div class="dropdown-item">
                    <div class="level">
                        <div class="level-left">
                            <div class="level-item has-text-white">
                                Notebook
                            </div>
                        </div>
                        <div class="level-right">
                            <div class="level-item">
                                <a> <i class="fas fa-plus has-text-white"></i> </a>
                            </div>
                        </div>
                    </div>
                </div>
                <hr class="dropdown-divider">

                <div class="dropdown-item">
                    <div class="level">
                        <div class="level-left">
                            <div class="level-item has-text-white">
                                Attributes(5)
                            </div>
                        </div>
                        <div class="level-right">
                            <div class="level-item">
                                <a> <i class="fas fa-plus has-text-white"></i> </a>
                            </div>
                        </div>
                    </div>
                </div>
                
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'bdl',
    props: {
        search: {
            type: String
        }
    },
    data: function(){
        return {
            toggle: false
        }
    },

    methods: {
        dropdownToggle: function(){
            var dropdown = document.querySelector('.dropdown');
            dropdown.classList.toggle('is-active');
            this.toggle = !this.toggle;
            var icon = document.getElementById('dropDownButton');
            if(this.toggle){
                icon.classList.remove('fa-plus');
                icon.classList.add('fa-minus');
            }
            if(!this.toggle){
                icon.classList.add('fa-plus');
                icon.classList.remove('fa-minus');
            }
        }
    }
}
</script>

<style scoped>
.dropdown-content{
    background: #7F3CD2;    
}
.dropdown-trigger{
     background: #7F3CD2;   
}
</style>