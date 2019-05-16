<template>
  <v-container fill-height>
    <v-layout row wrap align-center>
      <v-flex xs12>
        <v-toolbar flat></v-toolbar>
        <v-card>
          <div class="pa-3">
          <v-form
            ref="form"
            v-model="valid"
            lazy-validation
          >
            <v-text-field v-model="email" label="임시id" :rules="emailRules" required></v-text-field>
            <v-text-field v-model="password" label="임시pw" type="password" :rules="pwRules" required></v-text-field>
            <v-text-field v-model="name" label="이름" :rules="nameRules" required></v-text-field>
            <v-select v-model="age" :items="items" :rules="[v => !!v || 'Item is required']" label="나이" required ></v-select>
            <v-btn :disabled="!valid" large block color="primary" @click="signup()">회원가입</v-btn>
          </v-form>
          </div>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      valid: true,
      email: null,
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+[.].+/.test(v) || 'E-mail must be valid'
      ],
      password: null,
      pwRules: [
        v => !!v || 'Password is required',
        v =>  /([a-zA-Z0-9].*[!,@,#,$,%,^,&,*,?,_,~])|([!,@,#,$,%,^,&,*,?,_,~].*[a-zA-Z0-9])/.test(v) || '대소문자 숫자 *특수기호* (4~12)' 
      ],
      name: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 10) || 'Name must be less than 10 characters'
      ],
      age: null,
      select: null,
      items: []
    };
  },
  mounted () {
    for (let i = 10; i <= 50; i++) this.items.push(i)
  },
  methods: {
    signup() {
      axios.post("http://localhost:3000/api/user", {
          email: this.email,
          password: this.password,
          name: this.name,
          age: this.age
      })
      .then(r => {
        if (r.data.success) {
          alert("회원가입을 축하합니다.");
        }
        else {
          alert("회원가입 실패.");
        }
      })
      .catch(e => {
        console.error(e.message);
        alert(e.message);
      });
    },
  }
};
</script>
