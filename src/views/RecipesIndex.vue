<template>
  <div class="recipes-index">
    <h1>All Recipes</h1>
    <div>
      Filter Title: <input v-model="titleFilter" list="titles">

      <datalist id="titles">
        <option v-for="recipe in recipes">{{ recipe.title }}</option>
     <!--    <option>Burning Trash Dinner</option> -->
      </datalist>
    </div>

     
    
    <div class="row">
      <div class="col-md-4" v-for="recipe in filterBy(recipes, titleFilter, 'title')">
        <div class="card">
          <router-link v-bind:to="'/recipes/' + recipe.id">
            <img class="card-img-top" v-bind:src="recipe.image_url" v-bind:alt="recipe.title">
          </router-link>
          <div class="card-body">
            <h5 class="card-title">
              {{ recipe.title }}
            </h5>
          </div>
        </div>
      </div>
    </div>

     
  

  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');
import Vue2Filters from "vue2-filters";

export default {
  data: function() {
    return {
      recipes: [],
      currentRecipe: {},
      titleFilter: ""
    };
  },
  created: function() {
    axios.get("/api/recipes")
      .then(response => {
        this.recipes = response.data;
      });
  },
  methods: {
    
  },
  mixins: [Vue2Filters.mixin]
};
</script>