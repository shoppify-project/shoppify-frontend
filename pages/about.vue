<template>
	<v-card flat>
		<v-card-title>Текущая версия 1.0.2</v-card-title>
		<v-card-text>

		</v-card-text>
	</v-card>
</template>

<script>
export default {
	layout: "auth",
	auth: false,
	head: {
		title: "О проекте",
		meta: [
			{
				hid: "description",
				name: "description",
				content: "О проекте",
			},
		],
	},
	data: () => ({}),
};
</script>
