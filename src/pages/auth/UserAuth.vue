<template>
  <base-card>
    <form @submit.prevent="submitForm">
      <div class="form-controls">
        <label for="email">E-mail</label>
        <input type="email" id="email" required v-model.trim="email" />
      </div>
      <div class="form-controls">
        <label for="password">Password</label>
        <input type="password" required id="password" v-model.trim="password" />
      </div>
      <p v-if="!formIsValid">
        Please enter a valid email and password must be atleat six characters
        long
      </p>
      <base-button>{{ submitButtonCaption }}</base-button>
      <base-button type="button" mode="flat" @click="switchAuthMode">{{
        switchModeBuutonCaption
      }}</base-button>
    </form>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      formIsValid: true,
      mode: 'login',
    };
  },
  computed: {
    submitButtonCaption() {
      if (this.mode === 'login') {
        return 'Login';
      } else {
        return 'Signup';
      }
    },
    switchModeBuutonCaption() {
      if (this.mode === 'login') {
        return 'Signup instead';
      } else {
        return 'Login instead';
      }
    },
    methods: {
      submitForm() {
        if (
          !this.email === '' ||
          !this.email.includes('@') ||
          this.password.length < 6
        ) {
          this.formIsValid = false;
          return;
        }
        if (this.mode === 'login') {
          // login logic here
        } else {
          this.$store.dispatch('signup', {
            email: this.email,
            password: this.password,
          });
        }
      },
      switchAuthMode() {
        if (this.mode === 'login') {
          this.mode = 'signup';
        } else {
          this.mode = 'login';
        }
      },
    },
  },
};
</script>

<style scoped>
form {
  margin: 1rem;
  border-radius: 12px;
  padding: 1rem;
}

.form-control {
  margin: 0.5rem 0;
}

label {
  font-weight: bold;
  margin-bottom: 0.5rem;
  display: block;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  border: 1px solid #ccc;
  padding: 0.15rem;
}

input:focus,
textarea:focus {
  border-color: #3d008d;
  background-color: #faf6ff;
  outline: none;
}

.errors {
  font-weight: bold;
  color: red;
}
</style>
