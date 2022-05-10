<template>
  <q-page >
    <div v-if="agar">
      <q-input v-model="src" label="Rasm:" class="q-mr-xl q-ml-xl " maxlength="200" counter />
      <q-input v-model="fname" label="Ismingiz:" class="q-mr-xl q-ml-xl " maxlength="20" counter />
      <q-input v-model="text" label="Xabar:" class="q-mr-xl q-ml-xl " maxlength="1500" counter @keypress.enter="add" />
      <div style="width: 100%;" class="flex justify-end q-mt-lg">
        <q-btn color="blue" icon-right="send" label="Set" @click="add" class="q-mr-xl" />
      </div>
      <q-separator class="q-mt-lg"/>
    </div>

      <div class="col-12" v-if="agar">
        <q-item v-for="(people, i) in peoples" :key="people.id" class="col-12">
        <q-item style="width: 100%"  class="q-mb-sm 100%" clickable v-ripple v-if="people.agar" @click="oz(i)" >
          <q-item-section avatar>
            <q-avatar>
              <img :src="people.src" >
            </q-avatar>
          </q-item-section>

          <q-item-section>
            <q-item-label>{{ people.fname }}</q-item-label>
            <q-item-label caption lines="1">{{ people.massage }}</q-item-label>
            <q-separator class="q-mt-sm"/>
          </q-item-section>

          <q-item-section side>
            <q-icon name="chat_bubble" color="grey" />
          </q-item-section>
          <q-btn round color="deep-orange" icon="edit_location" class="q-ml-xl" @click="remove(i)" />
        </q-item>
        </q-item>

      </div>
      <div v-if="yoki">
        <div v-for="(people, i) in peoples" :key="people.id" v-show="people.yoki">
          <q-item clickable v-ripple v-if="people.yoki" class="col-12" @click="ortga(i)">
            <q-item-section avatar top>
            <q-avatar>
                <img :src="people.src" >
              </q-avatar>
            </q-item-section>

            <q-item-section>
              <q-item-label lines="1">{{ people.fname }}</q-item-label>
              <q-item-label caption>February 22nd, 2019</q-item-label>
            </q-item-section>

            <q-item-section side>
              <q-icon name="info" color="green" />
            </q-item-section>
          </q-item>
          <q-item>
           <div class="q-pa-md row justify-center col-12" >
            <div style="width: 100%;">
              <q-chat-message
                :text="['hey, how are you?']"
                sent
              />
              <q-chat-message
                :text="[ people.massage ]"
              />
            </div>
          </div>
          </q-item>
        </div>
      </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';
export default defineComponent({
  name: 'PageIndex',
  data() {
    return {
      src:"",
      fname:"",
      text:"",
      yoki:false,
      agar:true,
      peoples:[
        {src:"https://giftsluck.com/wp-content/uploads/2021/06/Red-Flowers-600x600.jpg", fname:"Guli",massage:"djbvcdsbnmkldfkjhb",agar:true,yoki:false}
      ]
    }
  },
  methods: {
    add(){
      const people={
        src:this.src,
        fname:this.fname,
        massage:this.text,
        agar:true,
        yoki:false
      }
      if(this.src.length==0 || this.fname.length==0 ||this.text.length==0){
        alert("Malumotlarni to'ldiring.")
      }
      else{
        this.peoples.unshift(people)
        this.src="",
        this.fname="",
        this.text=""
      }
    },
    remove(i){
       this.peoples.splice(i,1)
    },
    oz(i){
      this.peoples[i].agar=false
      this.peoples[i].yoki=true
      this.agar=false
      this.yoki=true
    },
    ortga(i){
      this.peoples[i].agar=true
      this.peoples[i].yoki=false
      this.agar=true
      this.yoki=false
    }
  },
})
</script>




