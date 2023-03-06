<template>
	<v-card flat>
		<v-card-title primary-title> Войти в панель </v-card-title>
		<v-card-text>
			<v-text-field
				v-model="login"
				:error-messages="nameErrors"
				label="Ваш логин"
				required
				@input="$v.login.$touch()"
				@blur="$v.login.$touch()"
			></v-text-field>

			<v-text-field
				v-model="password"
				:append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
				:type="show1 ? 'text' : 'password'"
				:error-messages="passwordErrors"
				label="и пароль"
				required
				@input="$v.password.$touch()"
				@blur="$v.password.$touch()"
				@click:append="show1 = !show1"
				v-on:keyup.enter="submit"
			></v-text-field>

			<v-btn
				:loading="loading"
				color="success"
				@click.prevent="submit"
				outlined
				block
			>
				Войти
			</v-btn>


      <vue-telegram-login 
    mode="callback"
    telegram-login="shoppify_team_bot"
    @callback="onTelegramAuth" />
		</v-card-text>

  
	</v-card>
</template>

<script>
import {vueTelegramLogin} from 'vue-telegram-login'
import { validationMixin } from "vuelidate";
import { required, maxLength } from "vuelidate/lib/validators";

export default {
	layout: "auth",
	components: {vueTelegramLogin},
	head: {
		title: "Вход",
		meta: [
			{
				hid: "description",
				name: "description",
				content: "Вход в админ панель",
			},
		],
	},
	data: () => ({
		loading: false,
		login: "",
		password: "",
		show1: "",
	}),
	// Validations
	mixins: [validationMixin],
	validations: {
		login: { required },
		password: { required },
	},
	// Computed
	computed: {
		nameErrors() {
			const errors = [];
			if (!this.$v.login.$dirty) return errors;
			!this.$v.login.required && errors.push("Введите логин");
			return errors;
		},
		passwordErrors() {
			const errors = [];
			if (!this.$v.password.$dirty) return errors;
			!this.$v.password.required && errors.push("Введите пароль.");
			return errors;
		},
	},
	// Methods
	methods: {
		onTelegramAuth (user) {
      // gets user as an input
      // id, first_name, last_name, username,
      // photo_url, auth_date and hash
      console.log(user)
    },
		// Метод сабмита формы
		async submit() {
			this.loading = true;
			// this.loading = true
			// Находим хеш из логина и пароля
			const payload = {
				login: this.login,
				password: this.password,
			};
			try {
				let response = await this.$auth.loginWith("local", { data: payload });
				console.log(response);
				this.loading = false;
			} catch (err) {
				this.$notifier.showMessage({
					content: "Неверный логин или пароль",
					color: "error",
				});
				this.loading = false;
			}
		},
	},
};
</script>
