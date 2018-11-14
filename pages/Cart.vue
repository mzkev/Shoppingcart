<template>
  <div class="cart">
    <h3 class="yourcart">YOUR CART</h3>
    <div @click="message=''" class="top-message" v-if="!!message">{{ message }}</div>
    <div v-for="(value, key) in cart" :key="key">
      <table>
        <tr>
          <td class="tdata">
      <img :src=items[key].url :alt=items[key].alt />
          </td>
        <td class="name-price">
        <div class="name"> {{ items[key].name }}</div>
        <span> Available in size 32, 34</span>
        <p class="price"> &#x20a6; {{ items[key].price }}</p>
        </td>
        <td>
        <span class="inc" @click="value > 0 ? updateCart(key, value, '-') : 0">-</span>
        <span> {{ value }}</span>
        <span class="inc" @click="updateCart(key, value, '+')">+</span>
        <span class="del" @click="$emit('delete-from-cart', key)">Remove</span>
        </td>
        </tr>
      </table>
      <hr />
    </div>
    <div class="tot">
    <span>Total</span>
    <span class="spantot"> &#x20a6;{{ total }}</span>
    </div>
    <div @click="$emit('close-cart')" class="hide-cart"> Continue Shopping</div>
  <div @click="postData" class="checkout">CHECKOUT</div>
  </div>
</template>

<script>
export default {
  props: ["cart", "items"],
  data() {
    return {
      counter: 1,
      message: ""
    };
  },
  methods: {
    getItem: function(item) {
      console.log(item, this.items);
      return this.items.find(({ id }) => id == item) || {};
    },
    deleteQuantity(index) {
      this.counter = 0;
      this.$emit("delete-from-cart", this.index);
    },
    postData: async function() {
      const res = await fetch(
        "http://www.mocky.io/v2/5be477442f00004900d9f521",
        {
          method: "POST"
        }
      ).then(res => res.json());
      console.log(res);
      this.message = res.message;
    },
    updateCart(index, value, type) {
      if (type === "+") {
        this.$emit("update-cart", index, ++value);
      } else {
        this.$emit("update-cart", index, --value);
      }
    }
  },
  computed: {
    total: function() {
      let total = 0;
      for (let x in this.cart) {
        total += this.cart[x] * this.items[x].price;
      }
      return total;
    }
  }
};
</script>

<style lang="scss">
.yourcart {
  text-align: center;
  padding: 3% 0%;
  background-color: whitesmoke;
}
.name-price {
  text-align: left;
}
.name {
  font-size: 18px;
  font-weight: bold;
}
.price {
  padding-top: 10px;
  font-size: 24px;
  font-weight: bold;
  color: #f5a623;
}
.tdata {
  width: 35%;
}
.inc {
  background-color: black;
  color: white;
  font-weight: bold;
  padding: 2%;
  margin: 0px 10px;
}
.tot {
  background-color: whitesmoke;
  margin: 40px auto;
  max-width: 600px;
  padding: 20px;
  font-weight: 500;
  font-size: 20px;
}
.spantot {
  float: right;
}
table {
  width: 100%;
  img {
    width: 30%;
    height: auto;
    margin-left: 30px;
  }
}
.cart {
  width: 100%;
  height: 100%;
  background-color: white;
  position: fixed;
  z-index: 1;
  display: block;
  overflow: hidden;
}

.hide-cart {
  padding-top: 10%;
  text-align: center;
  cursor: pointer;
}
.checkout {
  width: 100%;
  max-width: 400px;
  margin: 30px auto auto auto;
  padding: 20px 50px;
  background-color: #000000;
  color: beige;
  text-align: center;
  font: 30px bold;
}
.del {
  padding-top: 10px;
  color: red;
  display: block;
}
.top-message {
  position: fixed;
  top: 10px;
  left: 10%;
  width: 80%;
  background-color: #f5a623;
  padding: 30px;
  margin: auto;
  cursor: pointer;
  font-weight: bold;
  text-align: center;
}
</style>

