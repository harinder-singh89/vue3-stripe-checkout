<template>
  <div>
<!-- <h1>Home page</h1> -->
<p>{{formState.customerId}}</p>
<!--  -->


<Customer @customer-createsuccess="customerCreationSuccess" @create-customerfail="customerCreationFail"/>
  </div>
</template>
<script>
import { defineComponent,reactive} from 'vue'
import Customer from '../components/createCustomer.vue'

export default defineComponent({
  setup() {
    const formState = reactive({
      customerId:null
    })
    const customerCreationSuccess =(customerId)=> {
      console.log("hello")
      formState.customerId = customerId
      // window.alert(customerId)
          
        }
        const customerCreationFail =(error)=> {
      console.log("hello")
      formState.customerId = error
      // window.alert(error)
          
        }

        return{
          customerCreationSuccess,
          formState,
          customerCreationFail
        }

  },
  components: { 
    Customer
   }
})
</script>