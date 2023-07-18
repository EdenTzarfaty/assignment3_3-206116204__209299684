<template>
  <div class="container2" style="margin-left:140px; width: 1500px;">
    <h1 class="title" style="color: #1b1b1b; margin-bottom: -60px;margin-left: 550px; font-family: Agency FB,serif;font-size: 100px">My Recipes</h1>
    <section class="ReturnedRecipes" v-if="this.recipes !== ''">
      <b-container fluid class="recipe-container">
      <b-card-group  style="padding-top: 50px">
        <PreviewRecipe v-for="recipe in this.recipes"
                       :key="recipe.id"
                       :Recipe="recipe"
        ></PreviewRecipe>
      </b-card-group>
      </b-container>
    </section>
  </div>
</template>

<script>


import PreviewRecipe from "@/components/PreviewRecipe.vue";


export default {
  name: "MyRecipesPage",
  components: {
    PreviewRecipe
  },
  data() {
    return {
      recipes: ""
    };
  },
  mounted() {
    this.getMyRecipes();
  },
  methods: {
    async getMyRecipes() {
      try {
        const response = await this.axios.get(this.$root.store.server_domain + "/users/allRecipes", {withCredentials: true});
        this.recipes = response.data;
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>

<style>
.recipe-container {
  width: 800px;
  margin-left: -100px;
  padding: 30px;
  border-radius: 10px;
  color: black;
  font-family: "Agency FB", sans-serif;
  font-size: 25px;
}
</style>