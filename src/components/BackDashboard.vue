<template>
    <section class="m" style="background: #0F212C;" v-if="search">
      <div>
        <div class=" ml-5 mb-3 pt-3">
          <p class="has-text-white"> <span> <a> <i class="fas fa-chevron-circle-left"></i> </a></span> Back to Dashboard</p>
        </div>
        <div class="level pb-3">
          <div class="level-left ml-5">
            <div class="level-item">
              <p class="title is-6 has-text-white"> {{search}}</p>
            </div>
          </div>
          <div class="level-right mr-5">
            <span class="icon has-text-info mr-3"> <a> <i class="fas fa-download"></i> </a></span>
            <span class="icon has-text-info"> <a> <i class="fas fa-share-square"></i> </a> </span>
          </div>
        </div>
      </div>
      <hr id="hr" class="mx-5">
    </section>
</template>

<script>
export default {
  props: {
    search: {
      type: String
    }
  }
    
}
</script>

<style scoped>
#hr{
  margin-bottom: 100px;
  border: 0;
  height: 1px;
  background: white;
  opacity: 0.3;
}
</style>