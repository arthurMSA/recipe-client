<template>
	<v-card @click="showView = true" class="card-recipe" mix-height="200px">
		<v-card-title class="font-weight-bold  text-uppercase d-flex justify-space-between">
			<div class="align-end">
				{{ recipe.title }}
			</div>
			<div class="btn-icon">
				<v-btn class="btn-delete" icon @click="$emit('delete')">
					<v-icon>delete_outline</v-icon>
				</v-btn>
				<edit-modal class="btn-edit" :recipe="recipe" @edit="$emit('edit', $event)"/>
			</div>
		</v-card-title>
		<div class="divider mx-auto"></div>
		<v-card-text>
			{{ recipe.content }}
		</v-card-text>
		<view-modal :show="showView" @close="showView = !showView" :recipe="recipe"></view-modal>
	</v-card>
</template>
<script>
import EditModal from '@/components/modal/EditRecipe.vue'
import ViewModal from '@/components/modal/ViewRecipe.vue'

export default {
	components: {
		EditModal,
		ViewModal
	},
	props: {
		recipe: {
			type: Object,
			required: true
		}
  },
	data() {
		return {
			showView: false
		}
	}
}
</script>
<style scoped>
.card-recipe {
	border-radius: 4px;
}
.divider {
	border: 1px solid rgb(228, 228, 228);
	height: 1px;
	width: 98%;
}
.card-recipe:hover {
	    box-shadow: 0px 3px 6px -2px rgba(0,0,0,0.2), 0px 2px 7px 0px rgba(0,0,0,0.14), 0px 1px 10px 0px rgba(0,0,0,0.12);
			cursor: pointer;
}
.btn-icon {
	text-align: right;
	z-index: 10;
}
.btn-edit {
	z-index: 10;
}
.btn-delete {
	z-index: 11;
}
</style>