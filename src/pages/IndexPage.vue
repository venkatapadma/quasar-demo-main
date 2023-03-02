<template>
  <q-page class="flex flex-center">
    <CartC/>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import {CartC} from "../components/Cart.vue"
export default defineComponent({
  name: 'IndexPage',
  methods:{
    save:function(){
      console.log('test');
    }
  },components:{CartC}
})
</script>
