<template>
  <div class="menu-item">
    <img :src="image.source" :alt="image.alt" class="menu-item__image" />
    <div>
      <h3>{{ name }}</h3>
      <p v-if="onSale">Prix : {{ (price * 0.9).toFixed(2) }}<span> (10% de réduction !)</span></p>
      <p v-else>Prix : {{ price }}</p>
      <p v-if="inStock">En stock</p>
      <p v-else>En rupture de stock</p>
      <div v-if="inStock">
        <label for="add-item-quantity">Quantité : {{ quantity }}</label>
        <input id="add-item-quantity" type="number" v-model.number="quantity" />
        <BaseButton @click="updateShoppingCart(quantity)">Ajouter au panier</BaseButton>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
import BaseButton from "./BaseButton.vue";

export default {
  name: "MenuItem",
  components: { BaseButton },
  props: {
    image: {
      type: Object,
      required: true,
    },
    inStock: {
      type: Boolean,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    price: {
      type: Number,
      required: true,
    },
    quantity: {
      type: Number,
      defaut: 1,
    },
  },
  data() {
    return {
      onSale: false,
    };
  },
  methods: { ...mapActions(["updateShoppingCart"]) },
  beforeMount() {
    const currentDay = new Date().getDate();
    if (currentDay % 2 === 0) {
      this.onSale = true;
    }
  },
};
</script>

<style lang="scss">
.menu-item {
  display: flex;
  width: 500px;
  justify-content: space-between;
  margin-bottom: 30px;
  &__image {
    max-width: 300px;
  }
}
</style>
