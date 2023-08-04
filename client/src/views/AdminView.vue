<template>
  <main>
    <div>
      <input type="text" v-model="title" placeholder="Заголовок">
      <br>
      <input type="text" v-model="text" placeholder="Текст">
      <br>
      <input type="text" v-model="href" placeholder="Адрес ссылки">
      <br>
      <input type="text" v-model="src" placeholder="Имя картинки">
      <br>
      <input type="file" ref="upload" accept="image/jpeg, image/png" @change="previewFiles">
      <button @click="editSend(_id)" class="button">Save Edit</button>
      <button @click="add()" class="button">Add News</button>
      <br>
    </div>
    <div v-for="p of posts" :key="p._id">
      <h1>{{p.title}}</h1>
      <div class="flex">
        <div class="blogtext">
          <p>
            {{p.text}}
          </p>
          <a :href="p.href" class="button">Discover now</a>
          <button @click="del(p._id)" class="button">Delete</button>
          <button @click="editMethod(p._id)" class="button">Edit</button>
        </div>
        <div class="imgConteiner">
          <img :src="p.src" alt="">
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      posts: [],
      file: undefined,
      title: '', text: '', href: '', src: '', edit: false, _id: ''
    }
  },
  methods: {
    del: async function (_id) {
      await fetch('http://127.0.0.1:3002/posts', {
        method: "DELETE",
        headers: {
          'Content-Type': 'application/json;charset=utf-8'
        },
        body: JSON.stringify({ _id })
      })
      const i = this.posts.findIndex(n => n._id == _id)
      this.posts.splice(i, 1)
    },

    editMethod: function (_id) {
      const i = this.posts.findIndex(n => n._id == _id)
      this.edit = true
      this.title = this.posts[i].title
      this.text = this.posts[i].text
      this.href = this.posts[i].href
      this.src = this.posts[i].src
      this._id = this.posts[i]._id
    },
    editSend: async function (_id) {
      await fetch('http://127.0.0.1:3002/posts', {
        method: "PUT",
        headers: {
          'Content-Type': 'application/json;charset=utf-8'
        },
        body: JSON.stringify({ _id, title: this.title, text: this.text, href: this.href, src: this.src })
      })
      const i = this.posts.findIndex(n => n._id == _id)
      this.posts.splice(i, 1)
      this.posts.push({ _id, title: this.title, text: this.text, href: this.href, src: this.src })
      this.edit = false
      this.title = ''
      this.text = ''
      this.href = ''
      this.src = ''
      this._id = ''
    },
    previewFiles(event) {
			    console.log(event.target.files[0])
					this.file = event.target.files[0]
          this.src = event.target.files[0].name
		},
    add: async function () {
      if (this.file || this.src) {
        const fData = new FormData()
        fData.append('file', this.file)
        fData.append('title', this.title)
        fData.append('text', this.text)
        fData.append('href', this.href)
        fData.append('src', this.src)
        const result = await fetch('http://127.0.0.1:3002/posts', {
          method: "POST",
          body: fData,
        })
        const data = await result.json()
        console.log(data.result.insertedId)// TODO забрать _id, добавть в push
        this.posts.push({ title: this.title, text: this.text, href: this.href, src: this.src, _id: data.result.insertedId })
        this.edit = false
        this.title = ''
        this.text = ''
        this.href = ''
        this.src = ''
        this._id = ''
      }
    }
  },
  async beforeMount() {
    const data = await fetch('http://127.0.0.1:3002/posts')
    const posts = await data.json()
    this.posts = posts.all
  }
}
</script>

<style>
.blogtext {
  flex: 3;
}
</style>

<style scoped>
button {
  border: 0;
  width: 162px;
}

input {
  margin: 5px auto;
}
</style>
