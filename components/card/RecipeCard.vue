<template>
	<v-card>
		<v-card-title>
			{{ title }}
		</v-card-title>
		<v-card-text>
			{{ content }}
		</v-card-text>
	</v-card>
</template>
<script>
export default {
	props: {
		title: {
			type: String,
			required: false,
			default: "Sem título"
		},
		content: {
			type: String,
			required: true
		}
	}
}
</script>
<style scoped>
.card-recipe {
	border: 1px solid rgb(172, 172, 172);
}
</style>