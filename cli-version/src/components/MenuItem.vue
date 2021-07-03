<template>
  <div class="menu-item">
    <img :src="image.source" :alt="image.alt" class="menu-item__image" />
    <div>
      <h3>{{ name }}</h3>
      <p v-if="inStock">En stock</p>
      <p v-else>En rupture de stock</p>
      <div>
        <label for="add-item-quantity">Quantité : {{ quantity }}</label>
        <input id="add-item-quantity" type="number" v-model="quantity" />
        <button @click="addToShoppingCart(quantity)">Ajouter au panier d'achat</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MenuItem",
  props: ["addToShoppingCart", "image", "inStock", "name", "quantity"],
};
</script>

<style scoped lang="scss"></style>
