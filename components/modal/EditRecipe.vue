<template>
	<v-dialog
		max-width="500px"
		v-model="dialog"
	>
	   <template v-slot:activator="{ on }">
        <v-btn
          v-on="on"
					class="mb-2"
					flat
					icon
        >
				<v-icon>edit</v-icon>
        </v-btn>
      </template>
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
    recipe: {
      type: Object,
      required: true,
			default: {
				title: null,
				content: null
			}
    }
  },
	data() {
		return {
			dialog: null
		}
	},
	methods: {
		cancel() {
			this.dialog = false
		},
		async save(recipe) {
			recipe.title = recipe.title.toLowerCase()

			await this.$emit('edit', recipe)
			this.dialog = false
		}
	}
}
</script>