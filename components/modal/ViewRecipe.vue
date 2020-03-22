<template>
	<v-dialog
		max-width="500px"
		v-model="show"
	>
    <v-card>
      <v-card-title class="title">
        {{recipe.title}}
      </v-card-title>
      <v-card-text>
        <v-textarea
          :value="recipe.content"
          disabled
          auto-grow
          no-resize
        >
        </v-textarea>
      </v-card-text>
    </v-card>
	</v-dialog>
</template>
<script>
export default {
  props: {
    show: {
      type: Boolean,
      required: true,
      default: true
    },
    recipe: {
      type: Object,
      required: true
    }
  }
}
</script>