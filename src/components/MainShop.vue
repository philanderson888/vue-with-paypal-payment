<template>
  <div>
    <h1>Phil's Shop</h1>
    <div class="shopDisplay">
      <ul v-for="product in productArray" :key="product">
        <div class="shopItem">
          <p>
            <strong>{{product.description}}</strong>
          </p>
          <p>Price is £ {{product.price}}</p>
          <a v-bind:href="product.detail">
            <img width="200" :src="product.src" />
          </a>
        </div>
      </ul>
    </div>
    <div ref="paypal"></div>
    <form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top">
      <input type="hidden" name="cmd" value="_s-xclick" />
      <input type="hidden" name="hosted_button_id" value="NAA7PFGPDHHX8" />

      <input
        type="image"
        src="https://www.paypalobjects.com/en_GB/i/btn/btn_buynow_LG.gif"
        border="0"
        name="submit"
        alt="PayPal – The safer, easier way to pay online!"
      />
      <img
        alt
        border="0"
        src="https://www.paypalobjects.com/en_GB/i/scr/pixel.gif"
        width="1"
        height="1"
      />
    </form>
  </div>
</template>

<script>
export default {
  name: "MainShop",
  props: {
    msg: String
  },
  data: function() {
    return {
      loaded: false,
      paidFor: false,
      product: {
        price: 0.02,
        description: "a product",
        src: "https://picsum.photos/400/300?random=1",
        detail: "productdetail"
      },
      productArray: [
        {
          price: 0.03,
          description: "a wonderful product",
          src: "https://picsum.photos/400/300?random=2",
          detail: "productdetail"
        },
        {
          price: 0.04,
          description: "a great product",
          src: "https://picsum.photos/400/300?random=3",
          detail: "/productdetail"
        },
        {
          price: 0.05,
          description: "another product",
          src: "https://picsum.photos/400/300?random=4",
          detail: "/productdetail"
        },
        {
          price: 0.06,
          description: "a product",
          src: "https://picsum.photos/400/300?random=5",
          detail: "/productdetail"
        },
        {
          price: 0.03,
          description: "a wonderful product",
          src: "https://picsum.photos/400/300?random=2",
          detail: "/productdetail"
        },
        {
          price: 0.04,
          description: "a great product",
          src: "https://picsum.photos/400/300?random=3",
          detail: "/productdetail"
        },
        {
          price: 0.05,
          description: "another product",
          src: "https://picsum.photos/400/300?random=4",
          detail: "/productdetail"
        },
        {
          price: 0.06,
          description: "a product",
          src: "https://picsum.photos/400/300?random=5",
          detail: "/productdetail"
        },
        {
          price: 0.03,
          description: "a wonderful product",
          src: "https://picsum.photos/400/300?random=2",
          detail: "/productdetail"
        },
        {
          price: 0.04,
          description: "a great product",
          src: "https://picsum.photos/400/300?random=3",
          detail: "/productdetail"
        },
        {
          price: 0.05,
          description: "another product",
          src: "https://picsum.photos/400/300?random=4",
          detail: "/productdetail"
        },
        {
          price: 0.06,
          description: "a product",
          src: "https://picsum.photos/400/300?random=5",
          detail: "/productdetail"
        }
      ]
    };
  },
  mounted: function() {
    const script = document.createElement("script");
    script.src =
      "https://www.paypal.com/sdk/js?client-id=AZPdvg_8G7jFbXi83edJviH81Nb4PFcl2mTeYMWJhhn-PiCFBbhQ05gxq0_2ugz7j_zoumCEHl5nHGQe";
    script.addEventListener("load", this.setLoaded);
    document.body.appendChild(script);
  },
  methods: {
    setLoaded: function() {
      this.loaded = true;
      paypal
        .Buttons({
          createOrder: (data, actions) => {
            return actions.order.create({
              purchase_units: [
                {
                  description: this.product.description,
                  amount: {
                    currencyCode: "USD",
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.shopDisplay {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
}
.shopItem {
  width: 20vw;
  border: 1px solid black;
  padding-bottom: 2vh;
  margin: 2vmin;
}
</style>
