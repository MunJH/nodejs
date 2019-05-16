<template>
  <v-container fill-height>
    <v-layout row wrap align-center>
      <v-flex xs12>
        <v-toolbar flat></v-toolbar>
        <v-card>
          <div class="pa-3">
            <v-text-field v-model="email" label="임시id"></v-text-field>
            <v-text-field v-model="password" label="임시pw" type="password"></v-text-field>
            <v-btn large block color="primary" @click="signup()">회원가입</v-btn>
          </div>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      email: null,
      password: null
    };
  },
  methods: {
    signup() {
      axios
        .post("http://localhost:3000/api/user", {
          email: this.email,
          password: this.password
          // user: 'postMan'
        })
        .then(r => {
          this.pop("사용자 등록 완료");
          this.getUsers(); // 데이터갱신
        })
        .catch(e => {
          console.error(e.message);
          this.pop("e.message");
        });
    }
  }
};
</script>
