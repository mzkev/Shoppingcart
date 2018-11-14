<template>
<div>
  <div v-if="visible" class="overlay">
    <div class="center">
    <div @click="hideOverlay" class="hide-overlay">&times;</div>
    <img :src="item.url" :alt="item.alt"/>
    <h2 class="price-over">
      &#x20a6;{{item.price}}
    </h2>

    <div class="details">
    <h2>{{item.name }}</h2>

    <p>Available in size 32, 34 </p>
    </div>
    <div class="quantity">
      <button class="minus" @click="counter > 0 ? counter -= 1 : 0">-</button>
      <span class="quant-text">QUANTITY {{ counter }}</span>
      <button class="plus" @click="counter += 1">+</button>
    </div>
    <div>

    <button @click="updateQuantity" v-if="!isShowing" v-on:click="toggleShow" class="submit">
      Add to Cart
    </button>
    <button @click="deleteQuantity" v-if="isShowing" v-on:click="toggleShow" class="submit">
      Remove from Cart
    </button>
    </div>

    </div>
  </div><!--item-->
</div>
</template>



<script>
export default {
  props: ["item", "visible", "index"],
  data() {
    return {
      counter: 1,
      isShowing: false
    };
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing;
    },
    updateQuantity() {
      this.$emit("update-cart", this.index, this.counter);
    },
    deleteQuantity(index) {
      this.counter = 0;
      this.$emit("delete-from-cart", this.index);
    },
    hideOverlay() {
      this.counter = 1;
      this.isShowing = false;
      this.$emit("hide-overlay");
    }
  }
};
</script>

<style lang="scss">
.details {
  display: block;
  margin-top: 60px;
  padding-left: 3%;
}
.center {
  align-self: center;
  width: 100%;
  background-color: white;
  padding: 0% 0% 3% 2%;
  max-width: 400px;
  margin: auto;
  margin-top: 60px;
}
.overlay {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
  z-index: 2;
  display: block;
  overflow: hidden;

  .hide-overlay {
    float: right;
    background-color: black;
    color: white;
    cursor: pointer;
    padding: 10px;
    font-weight: 900;
    border-radius: 10%;
  }
}
.price-over {
  width: 130px;
  height: 50px;
  color: white;
  padding-top: 10px;
  margin: 15% 7% 0% 0%;
  background-color: black;
  text-align: center;
  float: right;
}

.minus {
  float: left;
  padding: 4% 5%;
  background-color: white;
  font-weight: bold;
  cursor: pointer;
}
.plus {
  float: right;
  padding: 4% 5%;
  background-color: white;
  font-weight: bold;
  cursor: pointer;
}
.quant-text {
  display: inline-block;
  text-align: center;
  width: 140px;
  padding: 8px;
  padding: 8px;
}

.submit {
  margin-left: 30px;
  width: 80%;
  margin-top: 10px;
  height: 40px;
  border: 2px;
  padding: 8px 13px;
  cursor: pointer;
  background: black;
  color: white;
  &:hover {
    opacity: 0.8;
    transition: 0.25s all ease-out;
  }
}

.quantity {
  display: inline-block;
  text-align: center;
  border: 0.5px solid black;
  margin-left: 30px;
  width: 80%;
  margin-top: 20px;
  background: #fff;
}
</style>
