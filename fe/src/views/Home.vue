<template>
  <v-container fluid>
    <v-slide-y-transition mode="out-in">
      <v-layout column align-center>
        <v-dialog v-model="dialog" width="500">
          <template v-slot:activator="{ on }">
            <v-btn color="red lighten-2" dark v-on="on">로그인 버튼</v-btn>
          </template>
          <v-card>
            <v-card-title class="headline grey lighten-2" primary-title>로그인</v-card-title>

            <v-card>
              <div class="pa-3">
                <v-text-field v-model="email" label="이메일을 입력하세요"></v-text-field>
                <v-text-field v-model="password" label="패스워드를 입력하세요" type="password"></v-text-field>
                <v-btn large block color="primary" @click="login()">로그인</v-btn>
              </div>
            </v-card>
            <v-divider></v-divider>
          </v-card>
        </v-dialog>
      </v-layout>
    </v-slide-y-transition>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      email: null,
      password: null,
      allUsers: []
    };
  },
  mounted() {
    this.getUsers();
  },
  methods: {
    login() {
      // 전체 유저에서 해당 이메일로 유저를 찾는다.
      let selectUser = null;
      this.allUsers.forEach(user => {
        if (user.email === this.email) selectUser = user;
      });

      if (selectUser) {
        if (selectUser.password == this.password) {
          alert("로그인 완료.");
          location.replace("/");
        } else {
          alert("이메일과 비밀번호가 일치하지 않습니다.");
        }
      } else {
        alert("존재하지 않는 계정입니다.");
      }
      // 그 유저의 비밀번호와 입력된 비밀번호를 비교한다.
    },
    getUsers() {
      axios
        .get("http://localhost:3000/api/user")
        .then(r => {
          this.allUsers = r.data.users;
          console.log(r);
        })
        .catch(e => {
          console.error(e.message);
        });
    }
  }
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>