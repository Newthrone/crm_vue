<template>
  <form class="card auth-card" @submit.prevent="subtitHandler">
    <div class="card-content">
      <span class="card-title">Домашняя бухгалтерия</span>
      <div class="input-field">
        <input id="email"
               type="text"
               :class="{invalid: ($v.email.$dirty && !$v.email.required) || ($v.email.$dirty && !$v.email.email)}"
               v-model.trim="email"/>
        <label for="email">Email</label>
        <small class="helper-text invalid"
               v-if="$v.email.$dirty && !$v.email.required"
               >
          Поле email не должно быть пустым
        </small>
        <small class="helper-text invalid"
               v-else-if="$v.email.$dirty && !$v.email.email"
               >
          Введите корректный Email
        </small>
      </div>
      <div class="input-field">
        <input id="password"
               type="password"
               class="validate"
               :class="{invalid: ($v.password.$dirty && !$v.password.required) || ($v.password.$dirty && !$v.password.minLength)}"
               v-model="password"/>
        <label for="password">Пароль</label>
        <small class="helper-text invalid" v-if="$v.password.$dirty && !$v.password.required">Введите пароль</small>
        <small class="helper-text invalid" v-else-if="$v.password.$dirty && !$v.password.minLength">Длина пароля быть минимум {{$v.password.$params.minLength.min }} символов. Сейчас он {{ password.length }}</small>
      </div>
    </div>
    <div class="card-action">
      <div>
        <button class="btn waves-effect waves-light auth-submit" type="submit">
          Войти
          <i class="material-icons right">send</i>
        </button>
      </div>
      <p class="center">
        Нет аккаунта?
        <router-link to="/register">Зарегистрироваться</router-link>
      </p>
    </div>
  </form>
</template>

<script>
  import {email, required, minLength} from 'vuelidate/lib/validators'
  export default {
    name: "Login",
    data: () => ({
      email: '',
      password: '',
    }),
    validations:{
      email: {email, required},
      password: {minLength: minLength(8), required},
    },
    methods: {
      subtitHandler() {
        if (this.$v.$invalid) {
          this.$v.$touch()
          return
        }
        const formData = {
          email: this.email,
          password: this.password,
        }
        console.log(formData)
        this.$router.push('/')
      }
    },
  };
</script>
