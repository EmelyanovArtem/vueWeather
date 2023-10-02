<template>
  <div class="wrapper">
    <div class="top-content-wrapper">
      <h2 class="subtitle">Добавить город</h2>
      <form class="form">
        <input @input="title = $event.target.value" type="text" class="input" placeholder="Москва">
        <button @click="addCity(title);  $event.preventDefault()" class="btn-sub">Добавить</button>
      </form>
    </div>
    <div class="posts">
      <div class="post" v-for="post in posts" :key="post.id">
        <h2 class="post-title">{{ post.response.location.name }} <br> {{ post.response.location.region}}</h2>
        <h3 class="">{{ post.response.current.temp_c }}°C</h3>
        <img :src="post.response.current.condition.icon" class="icon">
        <span class="text">Скорость ветра <strong>{{ post.response.current.wind_kph }}</strong> км/ч</span>
        <span class="text">Направление ветра <strong>{{ post.response.current.wind_dir }}</strong></span>
        <span class="text">Последнее обновление <strong>{{ post.response.current.last_updated }}</strong></span>
        <div class="btn-wrapper">
          <button @click="reloadApi(post)" class="btn-sub">Обновить</button>
          <button @click="hanldeDeletePost(post)" class="post-btn">Удалить</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const axios = require('axios').default;
let postsOnLoadPage;
if (JSON.parse(localStorage.getItem('posts'))){
  postsOnLoadPage = JSON.parse(localStorage.getItem('posts'));
} else{
  postsOnLoadPage = [];
}

export default {
  data() {
    return {
      posts: postsOnLoadPage,
      title: '',
    }
  },
  methods: {
      hanldeDeletePost(postForRemove) {
        this.posts = this.posts.filter(post => post !== postForRemove);
        localStorage.setItem('posts', JSON.stringify(this.posts))
      },
      addCity(city) {
        let posts = this.posts;
        axios.get(`http://api.weatherapi.com/v1/current.json?key=29c19b199002483eaaf130349232909&q=${city}&aqi=no`)
          .then(function (response) {
            posts.push({title: city, response:response.data})
            localStorage.setItem('posts', JSON.stringify(posts))
          })
      },
      reloadApi(post) {
        let posts = this.posts;
        axios.get(`http://api.weatherapi.com/v1/current.json?key=29c19b199002483eaaf130349232909&q=${post.response.location.name}&aqi=no`)
          .then(function (response) {
            post.response = response.data;
            localStorage.setItem('posts', JSON.stringify(posts))
          })
      }
  }
}
</script>

<style scoped>
.wrapper {
  width: 100%;
}

.top-content-wrapper {
  width: max-content;
  margin: 0 auto;
}
.form {
  display: flex;
  flex-direction: column;
  padding-bottom: 25px;
  margin-bottom: 50px;
  border-bottom: 2px solid rgb(160, 93, 223);
}
.input {
  width: 500px;
  padding: 10px 15px;
  font-size: 18px;
  margin-bottom: 15px;
}

.posts {
  display: flex;
  width: 100%;
  justify-content: center;
  flex-wrap: wrap;
}
.post {
  position: relative;
  display: flex;
  width: 350px;
  flex-direction: column;
  align-items: start;
  margin-bottom: 20px;
  border: 1px solid rgb(160, 93, 223);
  padding: 20px;
  color: white;
  text-align: left;
  margin-right: 50px;
}

.subtitle {
  margin-bottom: 55px;
  align-self: center;
}

.text {
  font-size: 20px;
  margin-bottom: 15px;
}

.icon {
  position: absolute;
  top: 5px;
  right: 5px;
}

.post-title {
  margin-bottom: 20px;
  font-size: 28px;
}

h3 {
  font-size: 24px;
  margin-bottom: 10px;
}

.post-btn {
  padding: 10px;
  background-color: transparent;
  color: rgb(231, 72, 72);
  border: 1px solid rgb(231, 72, 72);
  border-radius: 15px;
  font-size: 20px;
  align-self: flex-end
}

.btn-sub {
  padding: 10px 15px;
  color: white;
  background-color: transparent;
  border: 1px solid rgb(160, 93, 223);
  border-radius: 10px;
  font-size: 20px;
}

</style>