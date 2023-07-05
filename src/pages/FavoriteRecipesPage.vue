<template>
  <div class="container2" style="margin-left:140px; width: 1500px;">
    <h1 class="title" style="color: #1b1b1b; margin-bottom: -60px; font-family: Agency FB,serif;font-size: 100px">My Favorite Recipes</h1>
    <section style="margin-left: 180px" class="ReturnedRecipes" v-if="this.recipes !== ''">
      <b-card-group deck>
        <PreviewRecipe v-for="recipe in this.recipes"
                       :key="recipe.id"
                       :Recipe="recipe"
        ></PreviewRecipe>
      </b-card-group>
    </section>
  </div>
</template>

<script>


import PreviewRecipe from "@/components/PreviewRecipe.vue";


export default {
  name: "FavoriteRecipesPage",
  components: {
    PreviewRecipe
  },
  data() {
    return {
      recipes: ""
    };
  },
  mounted() {
    this.getMyFavoritesRecipes();
  },
  methods: {
    async getMyFavoritesRecipes() {
      try {
        console.log("MyFavoritesRecipes");
        const response = await this.axios.get(this.$root.store.server_domain + "/users/favorites", {withCredentials: true});
        this.recipes = response.data;
        console.log(this.recipes);
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>

<style>

</style>