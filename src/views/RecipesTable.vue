<template>
  <div class="recipes-index">
    <h1>All Recipes</h1>
    <div>
      Filter Title: <input v-model="titleFilter" list="titles">

      <datalist id="titles">
        <transition-group name="fade">
          <option v-for="recipe in recipes">{{ recipe.title }}</option>
        </transition-group>
      </datalist>
    </div>



    <table class="table table-striped table-primary">
      <thead class="thead-dark">
      <tr>
        <th scope="col" v-on:click="setSortAttribute('id')">ID
          <span v-if="sortAttribute === 'id' && sortOrder === 1">^</span>
          <span v-else-if="sortAttribute === 'id' && sortOrder === -1">v</span>
        </th>



        <th scope="col" v-on:click="setSortAttribute('title')">Title <!-- {{ orderIndicator ('title') }} --></th> 
        <th scope="col" v-on:click="setSortAttribute('chef')">Chef<span v-if="sortAttribute === 'chef'">*</span></th>
        <th scope="col" v-on:click="setSortAttribute('prep_time')">Prep Time<span v-if="sortAttribute === 'prep_time'">*</span></th>
      </tr>
      </thead>

      <tbody>
        <tr v-for="recipe in orderBy(filterBy(recipes, titleFilter, 'title'), sortAttribute, sortOrder)">
          <td>
            {{ recipe.id }}
          </td>
          <td>
            <router-link v-bind:to="'/recipes/' + recipe.id">
              {{ recipe.title }}
            </router-link>
          </td>
          <td>
            {{ recipe.chef }}
          </td>
          <td>
            {{ recipe.prep_time }}
          </td>
        </tr>
      </tbody>
    </table>

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
      titleFilter: '',
      sortAttribute: 'title',
      sortOrder: 1
    };
  },
  created: function() {
    axios.get("/api/recipes")
      .then(response => {
        this.recipes = response.data;
      });
  },
  methods: {
    setSortAttribute: function(inputAttribute) {
    },
  //   orderIndicator: function(inputAttribute) {
  //     if (this.sortAttribute === inputAttribute) {
  //       if (this.sortOrder === 1) {
  //         return "v";
  //     } else {
  //         return "^";
  //   } else {
  //       return " ";
  //   }
  // }
},
  mixins: [Vue2Filters.mixin]
};
</script>