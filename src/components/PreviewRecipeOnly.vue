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
            <b-icon-heart-fill style="font-size: 2rem;"></b-icon-heart-fill>
            <span> Likes:</span> {{ Recipe.popularity }}
          </li>
          <li>
            <b-icon-clock-history style="font-size: 2rem;"></b-icon-clock-history>
            <span> Time:</span> {{ Recipe.readyInMinutes }}
          </li>
          <li>
            <b-icon icon="egg" style="font-size: 2rem;"></b-icon>
            <span>Vegan:</span> {{ Recipe.vegan }}
          </li>
          <li>
            <b-icon-egg-fill style="font-size: 2rem;"></b-icon-egg-fill>
            <span>Vegetarian:</span> {{ Recipe.vegetarian }}
          </li>
          <li>
            <b-icon-x-circle-fill style="font-size: 2rem;"></b-icon-x-circle-fill>
            <span>Gluten-Free:</span> {{ Recipe.glutenFree }}
          </li>
          <li :href="getInstructions()"><span>Instructions: <br></span> {{ Instructions }}</li>

          <li>
            <span>Favorite:</span>
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" style="margin-left:10px"
                   v-if="favorited === true" checked disabled>
            <input class="form-check-input" type="checkbox" value="" @click="Favorite()" id="flexCheckDefault"
                   style="margin-left:10px" v-else-if="favorited !== true">
          </li>
          <li>
            <span>Watched:</span>
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" style="margin-left:10px"
                   v-if="watched === true" checked disabled>
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" style="margin-left:10px"
                   v-else-if="watched !== true" disabled>
          </li>
        </ul>
      </b-card-text>
    </b-card>
  </div>
</template>

<script>
import { faLeftRight } from "@fortawesome/free-solid-svg-icons";

export default {
  name: "PreviewRecipeOnly",
  props: {
    recipe_id: {
      type: Number,
      required: false
    },
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
      Instructions: '',
      favorited: false,
      watched: false
    };
  },
  mounted() {
    this.getFavorites();
  },
  methods: {
    async getFavorites() {
      try {
        console.log("getFavorite:" ,this.favorited)
        const response = await this.axios.get(this.$root.store.server_domain + "/users/favorites", { withCredentials: true });
        console.log("getFavorite2:" ,this.favorited)
        const recipesIDS = response.data;
        for (let i = 0; i < recipesIDS.length; i++) {
          if (recipesIDS[i] === this.Recipe.recipe_id) {
            this.favorited = true;
            return;
          }
        }
        this.favorited = false;
      } catch (error) {
        console.log(error);
      }
    },
    async Favorite() {
      try {
        //await this.getFavorites();
        console.log("favorite:" ,this.favorited)
        if (!this.favorited) {
          await this.axios.post(
            this.$root.store.server_domain + "/users/addFavoriteReciped/" + parseInt(this.Recipe.recipe_id),
            null,
            { withCredentials: true }
          );
          this.favorited = true;
        } else {
          this.favorited = false;
        }
        console.log("favorite2:" ,this.favorited)


      } catch (error) {
        console.log(error);
      }
    },
    getInstructions() {
      if (this.Recipe.analyzedInstructions === undefined && this.Recipe.instructions !== undefined) {
        this.Instructions = this.Recipe.instructions;
      } else {
        let returnedstring = "";
        for (let i = 0; i < this.Recipe.analyzedInstructions.length; i++) {
          returnedstring += "Part " + (i + 1) + ": ";
          for (let j = 0; j < this.Recipe.analyzedInstructions[i].steps.length; j++) {
            returnedstring += "Step " + (j + 1) + ": " + this.Recipe.analyzedInstructions[i].steps[j].step + " ";
          }
        }
        this.Instructions = returnedstring;
      }
    }
  }
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
}
</style>
