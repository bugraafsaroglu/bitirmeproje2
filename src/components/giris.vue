<template>
  <div>
    <img class="logo" src="../assets/users.png" />
    <h1>    ----------  𝐋𝐎𝐆𝐈̇𝐍  ----------</h1>
    <div class="form-container">
      <form @submit.prevent="login">
        <div class="form-group">
          <label for="username">Username:</label>
          <input type="text" id="username" v-model="username" class="form-control" required>
        </div>
        <div class="form-group">
          <label for="password">Password:</label>
          <input type="password" id="password" v-model="password" class="form-control" required>
        </div>
        <div class="form-group">
          <label for="captcha">Güvenlik Kodu:</label>
          <input type="text" id="captcha" v-model="captcha" class="form-control" required>
          <img :src="captchaImage" @click="refreshCaptcha" style="cursor: pointer;">cs
        </div>
        <button type="submit" class="btn btn-primary">Login</button>
        <div style="margin-top: 10px;"></div> <!-- Boşluk eklemek için -->
        <button type="button" @click="forgotPassword" class="btn btn-link">Şifremi Unuttum</button>
      </form>
      <div v-if="errorMessage" style="color: red; margin-top: 10px;">{{ errorMessage }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
      captcha: '',
      captchaImage: '',
      errorMessage: ''
    };
  },
  mounted() {
    this.refreshCaptcha();
  },
  methods: {
    login() {
      
      if (this.captcha.toLowerCase() === this.captchaValue.toLowerCase()) {
        alert('Giriş Başarılı!');
      } else {
        this.errorMessage = 'Güvenlik Kodu Yanlış.';
        this.refreshCaptcha();
      }
    },
    refreshCaptcha() {
     
      this.captchaValue = this.generateRandomCaptcha();
      this.captchaImage = `https://dummyimage.com/150x50/000/fff&text=${this.captchaValue}`;
      this.captcha = ''; 
    },
    generateRandomCaptcha() {
      
      let captcha = '';
      const possibleChars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
      for (let i = 0; i < 6; i++) {
        captcha += possibleChars.charAt(Math.floor(Math.random() * possibleChars.length));
      }
      return captcha;
    },
    forgotPassword() {
      alert('Şifrenizi sıfırlamak için lütfen e-posta adresinizi girin.');
    }
  }
};
</script>

<style scoped>
.logo {
  max-width: 150px;
  margin: 0 auto 20px;
  display: block;
}

.form-container {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
}

.form-group {
  margin-bottom: 15px;
}

.form-control {
  padding: 8px;
  width: 100%;
  box-sizing: border-box;
}

.btn {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}

.btn-primary {
  background-color: #007bff;
}

.btn-primary:hover {
  background-color: #0056b3;
}

.btn-link {
  color: #ffffff;
  background-color: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
  font-size: inherit;
  text-align: left;
}

.btn-link:hover {
  text-decoration: underline;
}

.small {
  font-size: 0.8rem;
  color: #6c757d;
}
</style>
