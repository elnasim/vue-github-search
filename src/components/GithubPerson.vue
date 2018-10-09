<template>
  <div class="github-person">
    <a class="person-link" :href="link" target="_blank">
      <div class="person-img" :style="'background-image: url(' + img + ')'"></div>
      <div class="person-name">{{login}}</div>
    </a>
    <div class="person-repo">
      <a :href="`https://github.com/${login}?tab=repositories`" class="person-repo-info" target="_blank">
        <span>Репозитории</span>
        <span>{{repos}}</span>
      </a>
      <a :href="`https://gist.github.com/${login}`" class="person-repo-info" target="_blank">
        <span>Гисты</span>
        <span>{{gists}}</span>
      </a>
      <a :href="`https://github.com/${login}?tab=followers`" class="person-repo-info" target="_blank">
        <span>Фолловеры</span>
        <span>{{followers}}</span>
      </a>
    </div>
  </div>
</template>

<script>
  export default {
    name: "GithubPerson",
    props: ['login', 'img', 'repos', 'gists', 'followers', 'link']
  }
</script>

<style scoped lang="scss">
  .github-person {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .person-link {
    text-align: center;
    color: #ffffff;
    text-decoration: none;
  }

  .person-img {
    width: 100px;
    height: 100px;
    border-radius: 100%;
    background-position: center;
    background-size: cover;
    background-color: #b0b0b0;
    margin-bottom: 15px;
  }

  .person-name {
    font-size: 24px;
  }

  .person-repo {
    display: flex;
    justify-content: space-between;
    width: 100%;
    margin-top: 30px;
  }

  .person-repo-info {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    font-size: 20px;
    width: 33.333%;
    color: #ffffff;
    text-decoration: none;
  }

  @media (max-width: 767px) {
    .person-repo{
      flex-direction: column;
      align-items: center;
    }
    .person-repo-info{
      margin-bottom: 40px;
      width: 100%;
      &:last-child{
        margin-bottom: 0;
      }
    }
  }
</style>
