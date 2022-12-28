<template>
    <div>
     
     <h1>Subscription Details</h1>
     <div>
        <h4>Name:{{formState.data.name}}</h4>
        <label>Price:</label> <span>999.00</span>
        <h3>
            Per Month
            Billed Monthly
          </h3>
          <button @click="Subscription()">subscribe</button>
     </div>
    </div>
</template>

<script>
import { defineComponent ,onMounted,reactive} from 'vue';
import { useRoute,useRouter } from 'vue-router';
import PostService from '../server/stripe-service'
export default defineComponent({
    components:{},
  
    setup(props,context){
        console.log(props,context)
        const route = useRoute();
        const router = useRouter();

    // Now you can access params like:
     
   const formState = reactive({
    data:{}

})
const Subscription = async()=>{
    console.log('sub')
    console.log(formState.data.cId,formState.data.pId)
    try {
        const res = await PostService.createSubs(
            formState.data.cId,
            formState.data.pId,
        )

        console.log(res)
        context.emit("subscriptionSuccess",res.data.clientSecret, )

        if (res.data) {
            window.alert("Subscription Created,Next step is complete the payment")
          
    router.push({ name: 'checkout', params: { clientSecret:res.data.clientSecret } })
      
        }

      } catch (error) {
        window.alert(error)
        context.emit("subscriptionFail",error )


        console.log(error.message)
     
      }

}
        onMounted(()=>{
    console.log(route.params);
    Object.assign(formState.data,route.params)

            
        })

        return{
            formState,Subscription

        }
    }
})

</script>