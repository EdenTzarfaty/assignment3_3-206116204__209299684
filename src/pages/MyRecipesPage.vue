<template>
  <div class="container2" style="margin-left:140px; width: 1500px;">
    <h1 class="title" style="margin-right:-250px; color: black">My Recipes</h1>
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
  name: "MyRecipes",
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
        const response = await this.axios.get(this.$root.store.server_domain + "/users/recipes");
        const RecipesData = response.data;
        this.recipes = RecipesData;
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