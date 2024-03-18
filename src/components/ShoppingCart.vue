<template>
    <div class="cart">
      <h2>Cart</h2>
      <div class="table-responsive">
        <table class="table">
          <thead>
            <tr>
              <th>Product</th>
              <th>Price</th>
              <th>Quantity</th>
              <th>Total</th>
              <th>Actions</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, index) in cart" :key="index">
              <td>{{ item.name }}</td>
              <td>&#8369;{{ item.price }}</td>
              <td>
                <div class="row">
                    <div class="col-4 col-md-8">
                        <input type="number" min="1" v-model="item.quantity" @change="updateQuantity(item, index)" class="form-control">
                    </div>
                    <div class="col-4 col-md-1">
                        <button @click="decrementQuantity(item, index)" class="btn btn-sm btn-outline-secondary btn-block">-</button>
                    </div>
                    
                    <div class="col-4 col-md-1">
                        <button @click="incrementQuantity(item, index)" class="btn btn-sm btn-outline-secondary btn-block">+</button>
                    </div>
                </div>

              </td>
              <td>&#8369;{{ item.total }}</td>
              <td>
                <button @click="removeFromCart(index)" class="btn btn-danger">Remove</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <h3 class="text-right"><strong>Total: &#8369;{{ total }} </strong></h3>
    </div>
  </template>
  

  <script>
  export default {
    props: ['cart'],
    computed: {
      total() {
        return this.cart.reduce((acc, item) => acc + item.total, 0);
      }
    },
    methods: {
      removeFromCart(index) {
        this.$emit('remove-from-cart', index);
      },
      updateQuantity(item, index) {
        if (item.quantity < 1 || isNaN(item.quantity)) {
          // Reset quantity to 1 if it's less than 1 or NaN
          item.quantity = 1;
        }
        this.$emit('update-quantity', { item, index });
      },
      decrementQuantity(item, index) {
        if (item.quantity > 1) {
          item.quantity--;
          this.updateQuantity(item, index);
        }
      },
      incrementQuantity(item, index) {
        item.quantity++;
        this.updateQuantity(item, index);
      }
    }
  }
  </script>
  