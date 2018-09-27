<template>
    <div v-if="!loading" class="row">
        <div class="card-group" v-for="(item, index) in items" :key="index">
            <div class="card"  style="width: 14rem;">
                <router-link tag="div" :to="{ path: '/item/' + item.id }">
                    <img class="card-img-top" :src="item.photo" alt="Card image cap">
                    <div class="card-body">
                        <h5 class="card-title">{{ item.title }}</h5>
                    </div>
                </router-link>
                <div class="card-footer">
                    <p class="card-text">${{ item.price }}</p>
                    <a @click="addToCart(item)" class="btn btn-primary">+ Add</a>
                </div>
            </div>
        </div>
    </div>
    <h1 v-else>Loading......</h1>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
        loading: true
    }
  },
  computed: {
      items(){
          return this.$store.getters.getInventory
      }
  },
  mounted() {
    this.fetchInventory()
  },
  methods: {
    addToCart(item) {
      this.$store.dispatch('addToCart', item)
    },
    fetchInventory() {
        var self = this
        axios.get("http://localhost:3000/items").then(response => {
        self.$store.commit('setInventory', response.data)
        self.loading = false
        })
  }
  }
}
</script>

<style>
.card {
  margin: 5px;
}
</style>
