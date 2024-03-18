<template>
    <div>
        <h1>Shopping Page</h1>
        <ProductList :products="products" @add-to-cart="addToCart" />
        <ShoppingCart :cart="cart" @remove-from-cart="removeFromCart" @update-quantity="updateQuantity" />
        <br>
        <div>
          <button type="button" class="btn btn-secondary" @click="handleLogout">Logout</button>
        </div>
        
    </div>
</template>

<script>

import ProductList from '@/components/ProductList.vue'


import ShoppingCart from '@/components/ShoppingCart.vue'


export default {

  components: {
    ProductList,
    ShoppingCart
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Hoodie', price: 10 },
        { id: 2, name: 'Blazer', price: 20 },
        { id: 3, name: 'Bra', price: 30 },
        { id: 4, name: 'Tshirt', price: 40 },
        { id: 5, name: 'Blouse', price: 30 },
        { id: 6, name: 'Dress', price: 25 },
        { id: 7, name: 'Crop top', price: 30 },
        { id: 8, name: 'Sweater', price: 35 },
        { id: 9, name: 'Socks', price: 30 },
        { id: 10, name: 'Pajama', price: 60 },
        { id: 11, name: 'Sando', price: 30 },
        { id: 12, name: 'Shorts', price: 20 },
        { id: 13, name: 'Pants', price: 23 },
        { id: 14, name: 'Jogging Pants', price: 22 },
        { id: 15, name: 'Trouser', price: 32 },
        { id: 16, name: 'Underwear', price: 21 },
        { id: 17, name: 'Polo', price: 22 },
        { id: 18, name: 'Coords', price: 44 },
        { id: 19, name: 'Coat', price: 22 },
        { id: 20, name: 'Jorts', price: 43 },
        { id: 18, name: 'Brief', price: 44 },
        { id: 19, name: 'Panty', price: 22 },
        { id: 20, name: 'Windbreaker', price: 43 },
        { id: 20, name: 'Jogger Pants', price: 43 }
      ],
      cart: []
    }
  },
  methods: {
    handleLogout() {
            localStorage.removeItem('token');
            this.$router.push('/login');
    },
    addToCart(product) {
      const index = this.cart.findIndex(item => item.id === product.id);
      if (index !== -1) {
        this.cart[index].quantity++;
        this.cart[index].total = this.cart[index].quantity * product.price;
      } else {
        this.cart.push({
          id: product.id,
          name: product.name,
          price: product.price,
          quantity: 1,
          total: product.price
        });
      }
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    },
    updateQuantity({ item, index }) {
      item.total = item.quantity * item.price;
      this.cart[index] = item; // Directly assign item to the array element
    }
  }
}
</script>