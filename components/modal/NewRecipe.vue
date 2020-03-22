<template>
	<v-dialog
		max-width="500px"
		v-model="show"
	>
		 <template v-slot:activator="{ on }">
        <v-btn
          v-on="on"
					class="mb-2"
					flat
					icon
        >
				<v-icon>add</v-icon>
        </v-btn>
      </template>
			<v-card>
				<v-card-title class="title">
					NOVA RECEITA
				</v-card-title>
				<v-card-text>
					<v-text-field
						v-model="recipe.title"
						placeholder="Nome da receita"
						solo
					/>
					<v-textarea
						v-model="recipe.content"
						placeholder="Digite aqui a sua receita"
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
		type: {
			type: String,
			required: false,
			default: 'new'
		},
		confirm: {
			type: Boolean,
			required: true,
			default: false
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
	watch: {
		show() {
			if(this.show){
				this.clean()
			}
		}
	},
	methods: {
		clean() {
			this.recipe.title = ""
			this.recipe.content = ""
		},
		cancel() {
			this.show = false
			this.clean()
		},
		async save(recipe) {
			if(recipe.title !== null && recipe.content !== null){

			  recipe.title = recipe.title.toLowerCase()
			  recipe.content = recipe.content.toLowerCase()

			  await this.$emit('create', recipe)
			  this.show = false
			}
		}
	}
}
</script>