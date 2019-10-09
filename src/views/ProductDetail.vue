<template>
  <div>
    <h1>Product detail</h1>
    <p>{{product.description}}</p>
    <p>Price is £ {{product.price}}</p>
    <img :src="product.src" />
    <div ref="paypal" class="paypal"></div>
  </div>
</template>
<script lang="ts">
import Vue from "vue";
export default {
  name: "ProductDetail",
  data: function() {
    return {
      loaded: false,
      product: {
        description: "Great product",
        price: 0.02,
        src: "https://picsum.photos/300/200?random=1"
      }
    };
  },
  mounted: function() {
    const script = document.createElement("script");
    script.src =
      "https://www.paypal.com/sdk/js?client-id=AdUqMkrW2rogd7xux-5XqctWLRHf7Up_qThlNfVban-mbK6EZQG6lIZbJVZq6wycIflPVaM4qfP7rndU";
    script.addEventListener("load", this.setLoaded);
    document.body.appendChild(script);
  },
  methods: {
    setLoaded: function() {
      this.loaded = true;
      window.paypal
        .Buttons({
          createOrder: (data, actions) => {
            return actions.order.create({
              purchase_units: [
                {
                  description: this.product.description,
                  amount: {
                    currencyCode: "GBP",
                    value: this.product.price
                  }
                }
              ]
            });
          }
        })
        .render(this.$refs.paypal);
    }
  }
};
</script>
<style scoped>
.paypal {
  width: 15vw;
  display: block;
  margin: auto;
}
</style>