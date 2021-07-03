<template>
  <div class="menu-item">
    <img :src="image.source" :alt="image.alt" class="menu-item__image" />
    <div>
      <h3>{{ name }}</h3>
      <p v-if="onSale">Prix : {{ (price * 0.9).toFixed(2) }}</p>
      <p v-else>Prix : {{ price }}</p>
      <p v-if="inStock">En stock</p>
      <p v-else>En rupture de stock</p>
      <div>
        <label for="add-item-quantity">Quantité : {{ quantity }}</label>
        <input id="add-item-quantity" type="number" v-model.number="quantity" />
        <button @click="addToShoppingCart(quantity)">Ajouter au panier d'achat</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MenuItem",
  props: ["addToShoppingCart", "image", "inStock", "name", "quantity", "price"],
  data() {
    return {
      onSale: false,
    };
  },
  beforeMount() {
    const currentDay = new Date().getDate();
    if (currentDay % 2 === 1) {
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
