<template>
<div>
  <div class="item">
    <img :src="url" :alt="alt"/>
    <h3 class="price">
      &#x20a6;{{price}}
    </h3>
    </div>
    <div class="below">
      <div class="name">
    <h3>{{ name }}</h3>
    </div>
    <button class="add" @click="$emit('add-to-cart', index)">
      <span> Add to Cart </span>
    </button>
    </div>
    <div>
</div>
    </div>
</template>


<script>
export default {
  props: ["id", "name", "url", "alt", "price", "isShowing", "index"]
};
</script>

<style lang ="scss">
.item {
  flex-direction: column;
  width: 350px;
  height: 330px;
  justify-content: space-around;
  background: #ffffff;
  margin: 30px 20px;

  .price {
    margin-top: 48px;
    width: 130px;
    height: 50px;
    color: white;
    padding-top: 10px;
    background-color: black;
    text-align: center;
    float: right;
  }
  img {
    align-self: center;
    max-width: 100%;
    height: auto;
  }
}
.below {
  display: inline-flex;
  float: right;
  padding-right: 40px;
  .name {
    padding-right: 50px;
  }
  .add {
    width: 100px;
    height: 40px;
    border: 2px;
    padding: 8px 13px;
    cursor: pointer;
    background: rgb(240, 188, 139);
    color: black;
    &:hover {
      opacity: 0.8;
      transition: 0.25s all ease-out;
    }
  }
}
</style>
