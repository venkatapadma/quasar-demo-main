<template>
   <div class="q-pa-md" style="max-width: 400px">

<q-form
  @submit="save()"
  @reset="onReset"
  class="q-gutter-md"
>
  <q-input
    filled
    v-model="item.name"
    label="Item Name *"
    hint="Name and surname"
    lazy-rules
    :rules="[ val => val && val.length > 0 || 'Please type something']"
  />

  <q-input
    filled
    type="number"
    v-model="item.price"
    label="Item Price *"
    lazy-rules
    :rules="[
      val => val !== null && val !== '' || 'Please type your age',
      val => val > 0 && val < 1000000 || 'Please type a real age'
    ]"
  />
  <div class="q-pa-md">
    <q-date
      v-model="item.date"
      landscape
    />
  </div>
  <q-toggle v-model="accept" label="I accept the license and terms" />

  <div>
    <q-btn label="Submit" type="submit" color="primary"/>
    <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
  </div>
</q-form>
</div>

  <div class="q-pa-md" style="max-width: 350px">
    <q-list bordered separator v-for="item in items" :key="item">
      <q-item>
        <q-item-section>
          <q-item-label>{{ item.name }}</q-item-label>
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ item.price }}</q-item-label>
        </q-item-section>
        <q-item-section>
          <q-btn
            class="glossy"
            round
            color="deep-orange"
            icon="local_activity"
          />
        </q-item-section>
      <q-item-section>
        <q-btn @click="del(item.id,index)">delete</q-btn>
    </q-item-section>
      </q-item>
    </q-list>
  </div>
</template>

<script>

export default {
  name: "CartC",
  data() {
    return {
      item:{
        name:'IPhone',
        price:1000,
        date:10-3-2020
      },
      items: [],
    };
  },
  methods:{
    async save(){
        const response = await fetch("http://localhost:3000/items",{
          method:'post', 
          body:JSON.stringify(Object.assign({},this.item)),
          headers:{
            'content-type':'application/json'
          }
        });
        this.items.push(await response.json())
      console.log('ajax');
    },
    async del(userid,index){
        const response1 = await fetch("http://localhost:3000/items",{
          method:'delete', 
          //body:JSON.stringify(Object.assign({},this.item)),
          // headers:{
          //   'content-type':'application/json'
          // }
        });
        this.items.splice(index,1);
      console.log('ajax');
      this.items.push(await response.json())
    }
  },
  mounted() {
    console.log("test");
    const promise = fetch("http://localhost:3000/items");
    promise.then((response) => {
      response.json().then((items) => (this.items = items));
    });
  },
};
</script>