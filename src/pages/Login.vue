<template>
  <div class="container">
    <div class="container__login">
      <img src="@/assets/logo.png" class="container__login__img" />
      <form class="container__login__form" @submit.prevent="submit">
        <input
          type="email"
          placeholder="Digite seu e-mail"
          class="container__login__form__input"
          v-model="email"
        />
        <input
          type="password"
          placeholder="Digite sua senha"
          class="container__login__form__input"
          v-model="senha"
        />
        <button class="container__login__form__button">Entrar</button>
      </form>

      <router-link to="/cadastro" class="container__login__cadastro"
        >Cadastre-se</router-link
      >
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      email: "",
      senha: "",
    };
  },
  methods: {
    async submit() {
      const { data } = await axios.get("http://localhost:3000/usuarios", {
        params: {
          email: this.enail,
          senha: this.senha,
        },
      });
      if (data.length > 0) {
        alert("logando..");
        this.$router.push("/");
      } else {
        alert("usuário ou senha incorretas");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  background: #212121;

  &__login {
    display: flex;
    justify-content: center;
    flex-direction: column;
    width: 30%;
    height: 100%;
    margin: 0 auto;
    &__img {
      width: 140px;
    }
    &__form {
      display: flex;
      flex-direction: column;
      &__input {
        outline: 0;
        border-radius: 5px;
        border: 0;
        padding: 15px;
        margin: 10px 0;
      }

      &__button {
        border: 0;
        padding: 15px;
        border-radius: 5px;
        background: #6202ee;
        color: #fff;
        font-weight: 500;
        font-size: 16px;
        cursor: pointer;
      }
    }
    &__cadastro {
      border: 1px solid #fff;
      text-decoration: none;
      color: #fff;
      padding: 15px;
      border-radius: 15px;
      margin-top: 10px;
      text-align: center;
      font-size: 16px;
      transition: 800ms;
      &:hover {
        background: #fff;
        color: #000;
      }
    }
  }
}
</style>
