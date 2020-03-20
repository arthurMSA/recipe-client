<template>
  <v-layout row wrap>
    <v-flex xs12>
      <v-text-field
        prepend-inner-icon="search"
        label="Buscar receita"
        solo
        :loading="true"
      />
    </v-flex>
    <v-flex>
      <recipe-card
        title="TESTE"
        content="OVO MEXIDOS COM SUCO DE LEITE E MARACUJA"
      />
    </v-flex>
  </v-layout>
</template>

<script>
import RecipeCard from '@/components/card/RecipeCard.vue'
export default {
  components: {
    RecipeCard
  }
}
</script>
