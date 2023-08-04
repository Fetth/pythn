<script setup>
import ButtonSlot from '@/components/ButtonSlot.vue'
import ButtonProps from '@/components/ButtonProps.vue'
import ButtonMix from '@/components/ButtonMix.vue'
</script>

<template>
  <main>
    <div class="flex">
      <div class="text">
        <h1>Philip Gilbert</h1>
        <div>You will begin to realise why this exercise is called the Dickens Pattern with reference to the ghost showing 
          Scrooge some different futures.
        </div>
        <div class="dropdown">
          <button class="button">Заказать звонок</button>
          <div class="dropdown-content">
            <input class="dropInput" type="tel" v-model="tel" placeholder="Ваш номер">
            <button class="button" @click="entry">Заказать звонок</button>
          </div>
        </div>
      </div>
      <div class="fsdfsd sdfsdfs" :[attr]="className" @click="attr=(attr=='class')?'style':'class'">
        <img src="@/assets/me.webp" alt="">
      </div>
    </div>
    <ButtonSlot>
      asasdоktgвок страницы
    </ButtonSlot>
    <ButtonProps :[textAtr]="buttonName" icon="🖂"/>
    <ButtonMix icon="🖂" @buttonClicked="myFunc">
      Button страницы
    </ButtonMix>
    <div class="forms">
      <form @submit.prevent="sendEmail">
        <input type="text" v-model="name" placeholder="Name" />
        <input type="email" v-model="email" placeholder="Email" />
        <button type="submit">Send</button>
      </form>
    </div>
  </main>
</template>

<script>
export default {
  data(){
    return {
      attr:'id',
      className: 'imgConteiner hgdgfhgfh',
      buttonName: 'sfgfdgfdgdg',
      textAtr: 'text',
      tel: '',
      name: '',
      email: '',
    } 
  },
  methods: {
    myFunc(a,b,c) {
      console.log('sdfsds', a,b,c)
    },
    entry() {
      alert("Ваш телефон: " + this.tel);
      this.tel = '';
    },
    sendEmail() {

      const link = `mailto:voronsuper@gmail.com?subject=Message from ${this.name}&body=${this.email}`;
      window.open(link);
      this.name = '';
      this.email = '';
    }  
  },
  watch: {
      // при каждом изменении `question` эта функция будет запускаться
      attr(newAttr, oldAttr) {
        console.log(oldAttr)
        console.log(newAttr)
      }
    },

}
</script>

<style>
</style>
