<template>
  <div>
    <b-card no-body v-bind:title="Recipe.title" img-top tag="article" style="max-width: 20rem;" class="mb-2">
      <router-link :to="{ name: 'RecipeViewPage', params:{id:Recipe.recipe_id} } ">
        <b-card-img :src="Recipe.image" />
      </router-link>
      <b-card-title v-bind:title="Recipe.title"></b-card-title>
      <b-card-text>
        <ul class="recipe-overview" style="list-style-type: none;">
          <li>
            <b-icon-clock-history style="font-size: 2rem;"></b-icon-clock-history>
            <span> Time:</span> {{ Recipe.readyInMinutes }}
          </li>
          <li>
            <b-icon-heart-fill style="font-size: 2rem;"></b-icon-heart-fill>
            <span> Likes:</span> {{ Recipe.popularity }}
          </li>
          <li>
            <b-icon icon="egg" style="font-size: 2rem;"></b-icon>
            <span>Vegan:</span> {{ Recipe.vegan }}
          </li>
          <li>
            <b-icon-egg-fill style="font-size: 2rem;"></b-icon-egg-fill>
            <span>Vegeterian:</span> {{ Recipe.vegetarian }}
          </li>
          <li>
            <b-icon-x-circle-fill style="font-size: 2rem;"></b-icon-x-circle-fill>
            <span>Gluten-Free:</span> {{ Recipe.glutenFree }}
          </li>
          <li>
            <span>Favorite:</span>
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" style="margin-left:10px"
                   v-if="this.favorited === true" checked disabled>
            <input class="form-check-input" type="checkbox" value="" @click="Favorite()" id="flexCheckDefault"
                   style="margin-left:10px" v-else-if="this.favorited !== true">
          </li>
          <li>
            <span>Watched:</span>
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" style="margin-left:10px"
                   v-if="this.watched === true" checked disabled>
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" style="margin-left:10px"
                   v-else-if="this.watched !== true" disabled>
          </li>
        </ul>
      </b-card-text>
    </b-card>
  </div>
</template>
  <script>
    export default {
      name: 'PreviewRecipe',
      props: {
        recipe_id: {
          type: Number,
          required: false
        }
        ,
        Recipe: {
          type: Object,
          required: false,
          default() {
            return undefined;
          }
        }
      },
        data() {
          return {
            favortied: this.favorited,
            watched: '',
          };
        },
        mounted() {
          this.getFavorites();
          this.getWatched();
        },
        methods: {
          //async getFavorites() {
          // try {
          //   const response = await this.axios.get(this.$root.store.server_domain+"/users/favorites",{withCredentials:true});
          //   const recipesIDS = response.data;
          //   //let recipes=RecipesData;
          //   for(let i = 0; i<recipesIDS.length;i++){
          //     if(recipesIDS[i] === this.recipe.id){
          //       this.favortied = true;
          //       return;
          //     }
          //   }
          //   this.favortied = '';
          // } catch (error) {
          //   console.log(error);
          // }
        },
        async Favorite() {
          // try {
          //   console.log(this.recipe.id)
          //   const response = await this.axios.post(this.$root.store.server_domain+"/users/addFavoriteReciped/" + this.recipe.id,
          //     {withCredentials:true}
          //   );
          //   this.favortied = true;
          // } catch (error) {
          //   console.log(error);
          // }
        },
        // async getWatched(){
        //   try {
        //     const response = await this.axios.get(this.$root.store.server_domain+"/users/user_indication_recipe_NEW",);
        //     const RecipesData = response.data;
        //     let recipes=RecipesData;
        //     for(let i = 0; i<recipes.length;i++){
        //       if(recipes[i] === this.recipe.id){
        //         this.watched = true;
        //         return;
        //       }
        //     }
        //     this.watched = '';
        //   } catch (error) {
        //     console.log(error);
        //   }
        // },
        // async Watch(){
        //   try {
        //     const parsed = JSON.stringify(this.recipe.id);
        //     this.$root.store.setQuery3(parsed);
        //     const response = await this.axios.post(this.$root.store.server_domain+"/users/user_watched_recipe",
        //       {
        //         recipeId: this.recipe.id
        //       }
        //     );
        //   } catch (error) {
        //     console.log(error);
        //   }
        // }
        //},

    };
  </script>

  <style lang="scss" scoped>
    b-card.title {
      color: blue;
    }

    div {
      margin-top: 10px;
      margin-right: 10px;
      margin-bottom: 10px;
      width: 310px;
      box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
      /* in order: x offset, y offset, blur size, spread size, color */
      /* blur size and spread size are optional (they default to 0) */

    }

  </style>

  <!--<style lang="scss" scoped>-->
  <!--.recipe-preview {-->
  <!--  display: inline-block;-->
  <!--  width: 90%;-->
  <!--  height: 100%;-->
  <!--  position: relative;-->
  <!--  margin: 10px 10px;-->
  <!--}-->
  <!--.recipe-preview > .recipe-body {-->
  <!--  width: 100%;-->
  <!--  height: 200px;-->
  <!--  position: relative;-->
  <!--}-->

  <!--.recipe-preview .recipe-body .recipe-image {-->
  <!--  margin: auto;-->
  <!--  display: block;-->
  <!--  width: 98%;-->
  <!--  height: auto;-->
  <!--  -webkit-background-size: cover;-->
  <!--  -moz-background-size: cover;-->
  <!--  background-size: cover;-->
  <!--}-->

  <!--.recipe-preview .recipe-footer {-->
  <!--  width: 100%;-->
  <!--  height: 50%;-->
  <!--  overflow: hidden;-->
  <!--}-->

  <!--.recipe-preview .recipe-footer .recipe-title {-->
  <!--  padding: 10px 10px;-->
  <!--  width: 100%;-->
  <!--  font-size: 12pt;-->
  <!--  text-align: left;-->
  <!--  white-space: nowrap;-->
  <!--  overflow: hidden;-->
  <!--  -o-text-overflow: ellipsis;-->
  <!--  text-overflow: ellipsis;-->
  <!--}-->

  <!--.recipe-preview .recipe-footer ul.recipe-overview {-->
  <!--  padding: 5px 10px;-->
  <!--  width: 100%;-->
  <!--  display: -webkit-box;-->
  <!--  display: -moz-box;-->
  <!--  display: -webkit-flex;-->
  <!--  display: -ms-flexbox;-->
  <!--  display: flex;-->
  <!--  -webkit-box-flex: 1;-->
  <!--  -moz-box-flex: 1;-->
  <!--  -o-box-flex: 1;-->
  <!--  box-flex: 1;-->
  <!--  -webkit-flex: 1 auto;-->
  <!--  -ms-flex: 1 auto;-->
  <!--  flex: 1 auto;-->
  <!--  table-layout: fixed;-->
  <!--  margin-bottom: 0;-->
  <!--  list-style-type: none;-->
  <!--  display: -webkit-box;-->
  <!--  display: -moz-box;-->
  <!--  display: -webkit-flex;-->
  <!--  display: -ms-flexbox;-->
  <!--  display: flex;-->

  <!--}-->

  <!--.recipe-preview .recipe-footer ul.recipe-overview li {-->
  <!--  -webkit-box-flex: 1;-->
  <!--  -moz-box-flex: 1;-->
  <!--  -o-box-flex: 1;-->
  <!--  -ms-box-flex: 1;-->
  <!--  box-flex: 1;-->
  <!--  -webkit-flex-grow: 1;-->
  <!--  flex-grow: 1;-->
  <!--  width: 90px;-->
  <!--  display: table-cell;-->
  <!--  text-align: center;-->

  <!--}-->



  <!--</style>-->