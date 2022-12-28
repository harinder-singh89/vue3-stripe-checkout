<template>
    <div>
  <h1>Create customer</h1>
  <!-- <p>{{formState}}</p> -->
  <div>
    <label>Name:</label> <input placeholder="Enter Name" type="text" v-model="formState.name"/> <br />
    <label>Email:</label> <input placeholder="Enter Email" type="email"  v-model="formState.email"/> <br />
    <button @click="createCustomer()">Submit</button>
    <p id="error">{{formState.error}}</p>


  </div>
    </div>
  </template>
  <script>
  import { defineComponent,reactive } from 'vue'
  
  import StripeService from '../server/stripe-service'
  import { useRouter } from "vue-router";

   
  
  export default defineComponent({
    components: {  },
    setup(props,context) {
      console.log(props)
        const formState = reactive({
            name:"",
            email:"",
            priceId:'price_1LkLDFSEvKMW8AqatEuvc1Rl',
            error:null
        })
        const router = useRouter()
        const createCustomer = async ()=>{
            console.log("hello")
            // router.push('plan')

            try {
           if(formState.name && formState.email){
            const res = await StripeService.createCust(formState.email, formState.name);
            console.log("res", res);
            context.emit('customerCreatesuccess',res.data.customer)
            window.alert("Customer is created !!")
            if(res.data.customer){
            router.push({ name: 'plan', params: { cId: res.data.customer,name:formState.name,pId:'price_1LkLDFSEvKMW8AqatEuvc1Rl' } })


            }
            
           }
           else{
            formState.error = "please correct Name or Email form fields"
            window.alert(formState.error)


           }
            // router.push('plan')
        
          } catch (error) {
            window.alert(error)
            context.emit('createCustomerfail',error)


            console.log(error);
           }
            // if(formState.name && formState.email){
            //     try {
            //         const res = await stripeService.createCust(formState.email,formState.name)
            //         console.log(res)
                    
            //     } catch (error) {
            //         console.log(error)
                    
            //     }
            // }
        }

        return{
            createCustomer,formState
        }
    },
  })
  </script>
  <style>
  #error{
    background-color: red;
   
    display: flex;
  justify-content: center;
  text-align: center;
  }
</style>