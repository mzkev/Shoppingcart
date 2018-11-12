<template>
<div>
  <div class="item">
    <img :src="url" :alt="alt" width="300" height="300"/>
    <h3 class="price">
      {{price}}
    </h3>
    </div>
    <div class="below">
      <div class="name">
    <h3>{{ name }}</h3>
    </div>
    <button @click="toggleShow(id)">
      <span v-if="isShowing"> Remove from Cart </span>
      <span v-else> Add to Cart </span>
    </button>
    </div>
    <div>
    <Child v-if="isShowing" class="item">
      <button @click="togle">
        X
      </button>
    </Child>
</div>
    </div>
</template>


<script>
import Child from "./Child.vue";
export default {
  props: ["id", "name", "url", "alt", "price"],
  components: {
    Child
  },
  data() {
    return {
      isShowing: false
    };
  },
  methods: {
    toggleShow(id) {
      this.isShowing = !this.isShowing;
      this.filters = Pictures.id != id;
    },
    togle() {
      this.isShowing = !this.isShowing;
    }
  }
};
</script>

<style scoped>
</style>
