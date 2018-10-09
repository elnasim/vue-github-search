<template>
  <div id="app">
    <div class="container">
      <Input :getData='getData'/>
      <GithubPerson
              v-if="isUserGetted"
              :link="link"
              :login="login"
              :img="img"
              :repos="repos"
              :gists="gists"
              :followers="followers"
      />
      <div class="text-error" v-if="isInputClear">Введите имя пользователя в поле выше</div>
      <div class="text-error" v-if="isUserNotFound">Пользователь с таким именем не найден</div>
    </div>
  </div>
</template>

<script>

  import Input from "./components/Input";
  import GithubPerson from "./components/GithubPerson";
  import axios from 'axios';
  import debounce from 'lodash/debounce';

  export default {
    name: 'app',
    components: {GithubPerson, Input},
    data() {
      return {
        login: '',
        img: '',
        repos: '',
        gists: '',
        followers: '',
        link: '',
        isInputClear: true,
        isUserGetted: false,
        isUserNotFound: false,
        isLoading: false,
      }
    },
    methods: {
      getData: debounce(function (userName) {
        axios.get(`https://api.github.com/users/${userName}`)
            .then(
                (data) => {
                  this.login = data.data.login;
                  this.img = data.data.avatar_url;
                  this.repos = data.data.public_repos;
                  this.gists = data.data.public_gists;
                  this.followers = data.data.followers;
                  this.link = data.data.html_url;
                  this.isUserGetted = true;
                  this.isInputClear = false;
                  this.isUserNotFound = false;
                  console.log('-->', data.data)
                },
                () => {
                  this.isUserNotFound = true;
                  this.isUserGetted = false;
                  this.isInputClear = false;
                }
            );
      }, 500)
    }
  }
</script>

<style lang="scss">
  body {
    margin: 0;
    padding: 0;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    color: #e3e6ed;
    background-color: #171c20;
  }

  #app {
    padding: 100px;
  }

  .container {
    max-width: 1200px;
    margin: auto;
  }

  .text-error {
    text-align: center;
    margin-top: 20px;
    font-size: 24px;
  }
</style>
