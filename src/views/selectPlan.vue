




<template>
    <div>
  
  
  
        <!--    -->

  <Subscription   @subscription-fail="subscriptionCreationFail" @subscription-success="subscriptionCreationSuccess"/>
    </div>
  </template>
  <script>
  import { defineComponent,reactive} from 'vue'
import Subscription from "../components/createSubscription.vue"
  
  export default defineComponent({
    setup() {
      const formState = reactive({
        data:null
      })
      const subscriptionCreationSuccess =(data)=> {
        console.log("hello")
        formState.data = data
        // window.alert(data)
            
          }
          const subscriptionCreationFail =(data)=> {
        console.log("hello")
        formState.data = data
        // window.alert(data)
            
          }
  
          return{
            subscriptionCreationSuccess,
            formState,
            subscriptionCreationFail
          }
  
    },
    components: { 
        Subscription,
        
     }
  })
  </script>