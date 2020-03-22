<template>
  <v-container>
    <v-layout row justify-center>
      <v-flex md12>
          <v-text-field
            class="mt-1"
            prepend-inner-icon="search"
            label="Buscar receita"
            solo
            @input="search($event)"
            :loading="!loaded"
          />
      </v-flex>
    </v-layout>
    <v-layout row justify-space-between>
      <v-flex class="title mb-3 mt-4">
        {{notFound ? 'Nenhuma receita encontrada' : 'SUAS RECEITAS' }}
        <modal-new @create="createRecipe($event)"/>
      </v-flex>
    </v-layout>
    <v-layout row wrap>
      <v-flex>
        <recipe-card
          v-for="(recipe, index) in recipes"
          :key="index"
          class="my-2"
          :recipe="recipe"
          @delete="deleteRecipe(recipe)"
          @edit="editRecipe(recipe)"
        />
      </v-flex>
    </v-layout>
    <!-- <modal-view :show="showModalView" :recipe="recipeToView" /> -->
  </v-container>
</template>

<script>
import RecipeCard from '@/components/card/RecipeCard.vue'
import ModalView from '@/components/modal/ViewRecipe.vue'
import ModalNew from '@/components/modal/NewRecipe.vue'
import ModalEdit from '@/components/modal/EditRecipe.vue'


export default {
  components: {
    RecipeCard,
    ModalView,
    ModalNew,
    ModalEdit
  },
  data() {
    return {
      recipes: [],
      loaded: false,
      notFound: false,
      showModalView: false,
      showModalEdit: false,
      recipeToView: {},
      recipeToEdit: {},
      confirmCreate: null
    }
  },
  created() {
    this.load()
  },
  methods: {
    async load()  {
      await this.$axios.$get('http://localhost:8080/api/v0/recipe')
      .then(res => {
        this.loaded = true
        this.recipes = res
      })
      .catch(err => console.err(err))
    },
    async createRecipe(recipe) {
      await this.$axios.$post('http://localhost:8080/api/v0/recipe', recipe)
      this.load()
    },
    async deleteRecipe(recipe) {
      await this.$axios.$delete('http://localhost:8080/api/v0/recipe/' + recipe.id)
      this.load()
    },
    async editRecipe(recipe) {
      await this.$axios.$put('http://localhost:8080/api/v0/recipe/' + recipe.id, recipe)
      this.load()
    },
    viewRecipe(recipe) {
      this.recipeToView = recipe
      this.showModalView = true
    },
    async search(value) {
      this.loaded = false
      await this.load()
      this.recipes =  this.recipes.filter(recipe => {
        if(recipe.title.indexOf(value.toLowerCase()) >= 0) {
          return recipe
        }

       } )
      if(this.recipes.length === 0) {
        this.notFound = true
      } else {
        this.notFound = false
      }
    }
  }
}
</script>
<style scoped>
</style>