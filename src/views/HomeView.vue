<template>
  <div class="home">
    <section class='hero is-medium is dark mb-6'>
      <div class='hero-body has-text-centered'>
        <p class="title mb-6">
          Welcome to MoreiraSteam
        </p>
        <p class="subtitle">
          The best game store online
        </p>
      </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centerede">
          Latest products
        </h2>
      </div>
      <!-- <div class="column is-3" 
         v-for="app in latestProducts"
         v-bindkey="app.id"
      >

         <div class="box">
          <figure class="image mb-4">
            <img :src="app.thumbnail">
          </figure>

          <h3 class="is-size-4">{{app.name}}</h3>
          <p class="is-size-6 has-text-grey">${{app.price}}</p>

            <router-link v-bind:to="app.get_absolute_url" class="button is-dark mt-4">View details</router-link>
        </div>
      </div> -->
      <ProductBox
        v-for="product in latestProducts"
        v-bind:key="product.id"
        v-bind:product="product"/>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import ProductBox from '@/components/ProductBox'
import ProductBox from '@/components/ProductBox.vue'

export default {
  name: 'HomeView',
  data(){
    return{
      latestProducts: []
    }
  },
  components: {
    ProductBox,
    ProductBox
},
  mounted(){
    this.getLatestProducts()

    document.title = 'Home  |  GameStore'

  },
  methods:{
    getLatestProducts(){
      axios
        .get('/api/v1/latest-products/')
        .then(response => {
          this.latestProducts = response.data
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>

