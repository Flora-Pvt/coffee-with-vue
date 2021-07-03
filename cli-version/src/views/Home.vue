<template>
  <div id="app" class="app">
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
        :addToShoppingCart="addToShoppingCart"
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
import MenuItem from "../components/MenuItem";

export default {
  name: "App",
  components: {
    MenuItem,
  },
  data() {
    return {
      restaurantName: "La belle Vue",
      simpleMenu: [
        {
          name: "Croissant",
          image: {
            source: "/images/croissant.jpg",
            alt: "Un croissant",
          },
          inStock: true,
          quantity: 1,
          price: 2.99,
        },
        {
          name: "Baguette de pain",
          image: {
            source: "/images/french-baguette.jpeg",
            alt: "Quatre baguettes de pain",
          },
          inStock: true,
          quantity: 1,
          price: 3.99,
        },
        {
          name: "Éclair",
          image: {
            source: "/images/eclair.jpg",
            alt: "Éclair au chocolat",
          },
          inStock: false,
          quantity: 1,
          price: 4.99,
        },
      ],
      itemsQuantityInCart: 0,
    };
  },
  computed: {
    copyright() {
      const currentYear = new Date().getFullYear();
      return `Copyright ${this.restaurantName} ${currentYear}`;
    },
  },
  methods: {
    addToShoppingCart(amount) {
      this.itemsQuantityInCart += parseInt(amount);
    },
  },
};
</script>
