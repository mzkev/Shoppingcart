<template>
  <div class="single">
    <img :src="url" :alt="alt" width="235" height="300"/>
    <h2>
      {{price}}
    </h2>
    <h2>{{ name }}</h2>
    <p>Available in size 32, 34 </p>
    <div class="quantity">
      <button class="inc" @click="counter > 0 ? counter -= 1 : 0">-</button>
      <span class="quant-text">Quantity {{ counter }}</span>
      <button class="inc" @click="counter += 1">+</button>
    </div>
    <button class="submit">Add to cart</button>
  </div><!--item-->
</template>



<script>
import Pictures from "./Pictures.vue";
export default {
  components: { Pictures },
  props: ["name", "url", "alt", "price"],
  data() {
    return {
      counter: 0
    };
  }
};
</script>

<style lang="scss">
.quant-text {
  display: inline-block;
  text-align: center;
  width: 140px;
  padding: 8px;
  padding: 8px;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 12px;
}

.quantity {
  border: 2px solid black;
  width: 235px;
  padding-left: 3px;
  border-radius: 1000px;
  background: #fff;
  margin-left: 20px;
}
.single {
  width: 350px;
  height: 800px;
  justify-content: space-around;
  background: #eee;
  padding: 20px 10px;
  margin: 30px;
}
</style>
