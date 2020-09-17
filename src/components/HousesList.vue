<template>
  <div id="app">
    <div class="container">
      <div class="row bg-light">
        <div class="mb-5 mt-5 col-sm-12 col-md-12">
          <div class="text-center p-3">
            <span class="font-weight-bold">
              <span class="mb-3 mt-3" style="color:#ef5777">
                <i class="fas fa-shopping-bag"></i> Wishlist:
              </span>
              <b class="text-dark">{{wishlist.length}}</b>
            </span>
            <br />
            <span class="font-weight-bold">
              <span class="mb-3 mt-3" style="color:#ef5777">
                <i class="fas fa-shopping-cart"></i> Shopping Cart:
              </span>
              <b class="text-dark">{{cart.length}}</b>
            </span>
            <hr />
            <span class="font-weight-bold form-inline mt-5" id="asidebar" style="color:#ef5777">
              <label for>Search by Price $</label>
              <input
                class="form-control w-5 mb-2 mt-2 border-top-0 border-right-0"
                type="number"
                min="0"
                max="200"
                v-model="price"
              />
            </span>
            <div class="mt-4">
              <label class="float-left">
                Min
                <b>$0</b>
              </label>
              <label class="float-right">
                Max
                <b>$200</b>
              </label>
              <input type="range" class="custom-range" min="0" max="200" v-model="price" />
            </div>
          </div>
        </div>
      </div>

      <hr />

      <div class="row mb-5">
        <div class="col-lg-3 col-md-4 col-sm-6 mb-3" v-for="item in products" :key="item.id">
          <div v-if="item.price <= Number(price)">
            <div>
              <div class="product-grid">
                <div class="product-image">
                  <img class="img-fluid d-block" :src="item.image" :alt="item.image_title" />
                  <ul class="social">
                    <li>
                      <a data-tip="Quick View" class="Quick-View">
                        <i class="fa fa-search"></i>
                      </a>
                    </li>
                    <li>
                      <a
                        data-tip="Add to WishList"
                        class="Add-to-Wishlist"
                        v-on:click="wishlist.push(item)"
                      >
                        <i class="fa fa-shopping-bag"></i>
                      </a>
                    </li>
                    <li>
                      <a class="add-to-cart" v-on:click="cart.push(item)" data-tip="Add to Cart">
                        <i class="fa fa-shopping-cart"></i>
                      </a>
                    </li>
                  </ul>
                  <span class="product-new-label">Sale</span>
                  <span class="product-discount-label">50%</span>
                </div>
                <ul class="rating">
                  <li class="fa fa-star"></li>
                  <li class="fa fa-star"></li>
                  <li class="fa fa-star"></li>
                  <li class="fa fa-star"></li>
                  <li class="far fa-star"></li>
                </ul>
                <div class="product-content">
                  <h3 class="title">
                    <a href="#">{{ item.name }}</a>
                  </h3>
                  <div class="price mb-4">
                    ${{Number(item.price)}}
                    <span>${{ (Number(item.price) + Number(item.price/2)).toFixed(2)}}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- footer -->
  <footer style="background-color: #2c292f">
    <div class="container">
      <div class="row">
        <div class="col-md-4 text-center text-md-left">
          <div class="py-0">
            <h3 class="my-4 text-white">
              About
              <span class="mx-2 font-italic" style="color:#ef5777">Alexis Store</span>
            </h3>

            <p class="footer-links font-weight-bold">
              <a class="text-white" href="#">Home</a>
              |
              <a class="text-white" href="#">Products</a>
              |
              <a class="text-white" href="#">About</a>
              |
              <a class="text-white" href="#">Contact</a>
            </p>
            <p class="text-light py-4 mb-4">&copy;Made with ❤️ by Alexis.</p>
          </div>
        </div>

        <div class="col-md-4 text-white text-center text-md-left">
          <div class="py-2 my-4">
            <div>
              <p class="text-white">
                <i class="fa fa-map-marker mx-2"></i>
                000 - Street Adddress,
                City, United States
              </p>
            </div>

            <div>
              <p>
                <i class="fa fa-phone mx-2"></i> 000-000-0000
              </p>
            </div>
            <div>
              <p>
                <i class="fa fa-envelope mx-2"></i>
                <a href="mailto:#">Contact@alexisStore.com</a>
              </p>
            </div>
          </div>
        </div>

        <div class="col-md-4 text-white my-4 text-center text-md-left">
          <span class="font-weight-bold">About the Company</span>
          <p
            style="color:#ef5777"
            class="my-2"
          >Lorem ipsum dolor sit amet consectetur, adipisicing elit. Architecto sint dolores, quibusdam maxime ex provident, autem voluptates officia.</p>
          <div class="py-2">
            <a href="#">
              <i class="fab fa-facebook fa-2x text-primary mx-3"></i>
            </a>
            <a href="#">
              <i class="fab fa-google-plus fa-2x text-danger mx-3"></i>
            </a>
            <a href="#">
              <i class="fab fa-twitter fa-2x text-info mx-3"></i>
            </a>
            <a href="#">
              <i class="fab fa-youtube fa-2x text-danger mx-3"></i>
            </a>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>


<script>
//import axios from 'axios'
export default {
  el: "#app",
  data() {
    //declaring var for live
    return {
      cart: [],
      wishlist: [],
      price: 200,
      products: null,
    };
  },
  mounted() {
    fetch("https://hplussport.com/api/products/order/price", {
      headers: {},
    })
      //getting dt as json
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
        console.log(data);
      });
  },
};
</script>