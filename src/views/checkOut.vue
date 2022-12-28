




<template>
  <div>




<Checkout @payment-Fail="paymentFail" @payment-success="paymentSuccess" />

  </div>
</template>
<script>
import { defineComponent,reactive} from 'vue'
import Checkout from "../components/checkoutComponent.vue"

export default defineComponent({
  setup() {
    const formState = reactive({
      data:null
    })
    const paymentSuccess =(data)=> {
      console.log("hello")
      formState.data = data
      // window.alert(data)
          
        }
        const paymentFail =(data)=> {
      console.log("hello")
      formState.data = data
      // window.alert(data)
          
        }

        return{
          paymentSuccess,
          formState,
          paymentFail
        }

  },
  components: { 
    Checkout
   }
})
</script>