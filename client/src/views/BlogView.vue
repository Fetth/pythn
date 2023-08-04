
<template>
  <!-- Основной контент -->
  <!-- <div :[attr]="login">
      <h1>About</h1>
  </div> -->
  <div class="post" v-for="post in posts" :key="post.id">
    <h1>{{ post.title }}</h1>
    <p>{{ post.text }}</p>

  </div>

</template>

<script>
// import компонентов
export default{
  // components: { // Подключаемые компоненты
  //     HelloWorld 
  // },
  data () {    // Переменные
      return {
          title: 'About',
          firrstName: '',
          lastName: '',
          attr: 'class',
          posts: [ ]
      }
  },
  methods: { // Наши функции
      create: function(){
          console.log('Hello!')
      },
      async getPosts(){
         
      }
  },
  computed: { // Метод который содержит обьект с вычисляемыми свойствами
      fullName() {
          return this.firrstName + this.lastName 
      },
  },
  watch: { // Содержит обьект с наблюдателями за изменениями

  },
  async mounted() { // Компонент монтирован
      const data = await fetch('http://127.0.0.1:8000/api/posts/')
      this.posts = await data.json()
  },
  updated() {

  },
  created() {

  },
  unmounted() {

  },
  beforeMount() {
      
  }
}
</script>

<style scoped> 
.post{
  
  width: 400px;
  height: max-content;
  margin-top: 10px;
  margin-left: auto;
  margin-right: auto;
  color: black
}
</style>