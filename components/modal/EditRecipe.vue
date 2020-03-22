<template>
	<v-dialog
		max-width="500px"
		v-model="show"
	>
			<v-card>
				<v-card-title class="title">
					EDITAR RECEITAR
				</v-card-title>
				<v-card-text>
					<v-text-field
						v-model="recipe.title"
						:value="recipe.title"
						placeholder="Titulo da receita"
						solo
					/>
					<v-textarea
						v-model="recipe.content"
						:value="recipe.content"
						auto-grow
						solo
					/>
				</v-card-text>
				<v-card-actions>
					<v-spacer></v-spacer>
					<v-btn
						flat
						color="red"
						@click="cancel()"
					>
						CANCELAR
					</v-btn>
					<v-btn
						color="green"
						outlined
						flat
						@click="save(recipe)"
					>
						SALVAR
					</v-btn>
				</v-card-actions>
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
  },
	data() {
		return {
			show: null,
			recipe: {
				title: null,
				content: null
			}
		}
	},
	methods: {
		clean() {
			this.recipe.title = ""
			this.recipe.content = ""
		},
		cancel() {
			this.clean()
		},
		async save(recipe) {
			recipe.title = recipe.title.toLowerCase()
			recipe.content = recipe.content.toLowerCase()

			await this.$emit('edit', recipe)
			this.show = false
		}
	}
}
</script>