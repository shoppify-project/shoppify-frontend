<template>
	<v-app id="inspire">
		<v-app-bar app color="primary" flat dark>
			<v-avatar
				:color="$vuetify.breakpoint.smAndDown ? 'grey darken-1' : 'transparent'"
				size="32"
			></v-avatar>

			<v-tabs centered class="ml-n9" color="white">
				<v-tabs-slider color="warning"></v-tabs-slider>

				<v-tab
					exact-active-class=""
					v-for="link in links"
					:key="link"
					:to="{ path: link.url }"
					exact
				>
					{{ link.name }}
				</v-tab>
			</v-tabs>

			<!-- <v-avatar
				class="hidden-sm-and-down"
				color="grey darken-1 shrink"
				size="32"
			></v-avatar> -->
		</v-app-bar>

		<v-main class="grey lighten-3">
			<v-container>
				<v-row>
					<v-col cols="12" sm="7">
						<v-sheet min-height="10vh" rounded="lg">
							<v-img :src="require('~/assets/04.jpg')"></v-img>
						</v-sheet>
					</v-col>

					<v-col cols="12" sm="5">
						<v-sheet min-height="70vh" rounded="lg">
							<Nuxt />
						</v-sheet>
					</v-col>
				</v-row>
			</v-container>
		</v-main>
	</v-app>
</template>

<script>
export default {
	data: () => ({
		links: [
			{ name: "Вход в систему", url: "/login" },
			{ name: "Ver 1.2", url: "/about" },
		],
	}),
};
</script>
