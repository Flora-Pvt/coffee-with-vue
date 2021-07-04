<template>
  <div>
    <h1>{{ restaurantName }}</h1>
    <p class="description">
      Bienvenue dans notre café {{ restaurantName }} ! Nous sommes réputés pour notre pain et nos merveilleuses pâtisseries. Faites vous plaisir dès
      le matin ou avec un goûter réconfortant. Mais attention, vous verrez qu'il est difficile de s'arrêter.
    </p>

    <section class="menu">
      <h2>Menu</h2>
      <MenuItem
        v-for="item in simpleMenu"
        :key="item.name"
        @add-items-to-cart="addToShoppingCart"
        :name="item.name"
        :image="item.image"
        :price="item.price"
        :quantity="item.quantity"
        :inStock="item.inStock"
      />
    </section>

    <aside class="shopping-cart">
      <!-- prend le nombre de l'input et l'ajoute au nombre du panier -->
      <h2>Panier d'achat: {{ itemsQuantityInCart }} articles</h2>
    </aside>

    <footer class="footer">
      <p>{{ copyright }}</p>
    </footer>
  </div>
</template>

<script>
import { mapGetters, mapState } from "vuex";
import MenuItem from "../components/MenuItem";

export default {
  name: "App",
  components: {
    MenuItem,
  },
  computed: {
    ...mapState({ itemsQuantityInCart: "itemsQuantityInCart", restaurantName: "restaurantName", simpleMenu: "simpleMenu" }),
    ...mapGetters({ copyright: "copyright" }),
  },
  methods: {
    addToShoppingCart(amount) {
      this.itemsQuantityInCart += amount;
    },
  },
};
</script>

<style lang="scss">
.description {
  max-width: 960px;
  font-size: 1.2rem;
  margin: 0 auto;
}

.menu {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.shopping-cart {
  position: absolute;
  right: 30px;
  top: 0;
}

.footer {
  text-align: center;
  font-style: italic;
}
</style>
