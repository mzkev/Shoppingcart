<template>
  <div class="full">
    <div>
      <Overlay :visible="overlayVisible" :index="activeItem" @hide-overlay="hideOverlay" @update-cart="updateCart"
        :item="items[activeItem]" @delete-from-cart="deleteFromCart" />
    </div>
    <div>
      <div @click="cartShow" class="cartsho">
        <span v-if="isShowingCart"></span>
        <div v-else style="width:30px">
          <img src="./cart.png" alt="cart" width="20px" /><span class="total">{{ total }}</span>
        </div>
      </div>
      <Cart v-if="isShowingCart" @close-cart="closeCart" :cart="cart" :items="items"  @update-cart="updateCart" @delete-from-cart="deleteFromCart"/>
    </div>
    <div class="upper">
      <h1 class="ash">ASHLUXURY</h1>
      <h2 class="fashion"> Fashion &amp; Lifestyle 📧 admin@ashluxury.com 📲
        whatsapp: +234 8169761216 🌍 worldwide shipping
        📍22B Admiralty Way 🕙HQ opens 10am - 8pm (mon-sat)</h2>
    </div>
    <div id="app">
      <div v-for="(item, index) in items" :key="item.id">
        <Picture @add-to-cart="addToCart" class="picture" :id="item.id" :index="index" :name="item.name" :url="item.url"
          :alt="item.alt" :price="item.price"></Picture>
      </div>
    </div>
    <div class="rectangle">See More</div>
    <div class="rectangle-2">Follow Us On Instagram</div>
  </div>
</template>

<script>
import Picture from "../components/Picture.vue";
import Overlay from "../components/Overlay";
import Cart from "./Cart";
import items from "../components/items";

export default {
  name: "app",
  components: {
    Picture,
    Overlay,
    Cart
  },
  methods: {
    addToCart: function(index) {
      this.activeItem = index;
      console.log("Active item", this.activeItem, index);
      this.overlayVisible = true;
      if (!this.cart[index]) {
        this.cart = { ...this.cart, [index]: 1 };
      } else {
        this.cart = { ...this.cart, [index]: this.cart[index]++ };
      }
    },
    cartShow() {
      this.isShowingCart = true;
    },
    closeCart() {
      this.isShowingCart = false;
    },
    deleteFromCart: function(index) {
      const cart = { ...this.cart };
      delete cart[index];
      this.cart = cart;
      console.log("Deleting", this.cart, index);
      // this.cart = this.$delete = this.activeItem[index];
    },
    hideOverlay: function() {
      this.overlayVisible = false;
    },
    updateCart: function(id, count) {
      console.log(id, count);
      const newCart = { ...this.cart };
      newCart[id] = count;
      this.cart = newCart;
    }
  },
  data() {
    return {
      overlayVisible: false,
      activeItem: -1,
      cart: {},
      items,
      isShowingCart: false
    };
  },
  computed: {
    total: function() {
      return Object.values(this.cart).reduce((i, v) => i + v, 0);
    }
  }
};
</script>

<style lang="scss">
body {
  font-family: SFUIText;
}
#app {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 0px 30px;
}
.upper {
  padding-top: 60px;
}
.total {
  background-color: #f5a623;
}
.cartsho {
  padding-right: 20%;
  margin-left: 80%;
  padding-top: 5%;
  float: right;
  cursor: pointer;
}

.full {
  padding-bottom: 30px;
  background-color: #ede3d8;
  width: 100%;
}
.picture {
  justify-content: center;
}

.ash {
  font-size: 48px;
  color: #333333;
  @extend .special;
}

.fashion {
  width: 100%;
  padding: 5px 15px;
  max-width: 600px;
  font-size: 20px;
  color: #4a4a4a;
  @extend .special;
}

.special {
  font-family: SFUIText;
  font-weight: 500;
  font-style: normal;
  font-stretch: normal;
  line-height: normal;
  letter-spacing: 0px;
  text-align: left;
}
.rectangle {
  width: 100%;
  margin: 20px auto;
  max-width: 150px;
  border: solid 4px #000000;
  text-align: center;
  padding: 60px 0px 0px 0px;
}
.rectangle-2 {
  width: 100%;
  margin: 0px auto;
  max-width: 400px;
  height: 70px;
  background-color: #000000;
  color: beige;
  text-align: center;
  font: 30px bold;
  padding-top: 12px;
}

h3,
li {
  @extend .special;
}

h2 {
  font-size: 20px;
  text-align: left;
}
</style>
