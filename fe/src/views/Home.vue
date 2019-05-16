<template>
  <v-container fluid>
    <v-slide-y-transition mode="out-in">
      <v-layout column align-center>
        <img src="@/assets/logo.png" alt="Vuetify.js" class="mb-5">
        <blockquote>
          &#8220;First, solve the problem. Then, write the code.&#8221;
          <footer>
            <small>
              <em>&mdash;John Johnson</em>
            </small>
          </footer>
        </blockquote>
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

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" flat @click="dialog = false">I accept</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-layout>
    </v-slide-y-transition>
  </v-container>
</template>

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