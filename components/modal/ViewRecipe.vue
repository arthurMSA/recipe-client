<template>
	<v-dialog
		max-width="500px"
		v-model="show"
	>
    <v-card>
      <v-card-title class="title d-flex">
        <v-flex>
          {{recipe.title}}
        </v-flex>
        <v-flex style="text-align: right">
          <v-btn
           @click="$emit('close', !show)"
           icon
          >
            <v-icon>close</v-icon>
          </v-btn>
        </v-flex>
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
    recipe: {
      type: Object,
      required: true,
      default: {
        title: null,
        content: null
      }
    },
    show: {
      type: Boolean,
      required: true,
      default: false
    }
  }
}
</script>