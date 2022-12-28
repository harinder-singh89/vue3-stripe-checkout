<template>
    <div>
        <h1>checkout page</h1>
        <!-- <p>{{formState}}</p> -->
        <div id="card"></div>
        <button disable="formState.disabled" @click="payment()">Complete Payment</button>
        <p id="error">{{formState.error}}</p>
    </div>
</template>
<script>
import { defineComponent ,onMounted,reactive} from 'vue';
import { useRoute,useRouter } from 'vue-router';
import { loadStripe } from "@stripe/stripe-js";


export default defineComponent({

setup(props,context){
    console.log(props,context)
    const route = useRoute()
    const router = useRouter()
    const formState = reactive({
        data:{}
    })
    const proFeaturesData = reactive({
      
     
      card: null,
      stripe: null,
      amount: null,
      plandId: null,
      loader: false,
      state: false,
      error:null,
      disabled:false
      
      
    })
    onMounted(()=>{
        renderCard()
        console.log(route.params)
        Object.assign(formState.data,route.params)
    })
    const renderCard = async () => {
      // let stripe = null;

      let elements = null;
      // var card = null;
      // console.log("hello");
      const ELEMENT_TYPE = "card";

      proFeaturesData.stripe = await loadStripe(
        "your_stripe_public_key"
      );
      // this.publishableKey = "";

      elements = proFeaturesData.stripe.elements();
      proFeaturesData.card = elements.create(ELEMENT_TYPE, {
        base: {
          color: "#32325d",
          fontFamily: '"Helvetica Neue", Helvetica, sans-serif',
          fontSmoothing: "antialiased",
          fontSize: "16px",
          "::placeholder": {
            color: "#aab7c4"
          }
        },
        invalid: {
          color: "#fa755a",
          iconColor: "#fa755a"
        }
      });
      proFeaturesData.card.mount("#card");
    };

    const payment = async()=>{
        formState.disabled=true
        console.log(formState.data.clientSecret)
        await proFeaturesData.stripe
        .confirmCardPayment(formState.data.clientSecret, {
          payment_method: {
            type: "card",
            card: proFeaturesData.card,
            billing_details: {
              name: "fullName"
            }
          }
        }).then((res)=>{
            console.log(res)
            if(res.error){
            context.emit('paymentFail',res.error)

        formState.disabled=false
        window.alert(res.error.message)

                formState.error=res.error.message
            }
            else{
                
            context.emit('paymentSuccess',res.paymentIntent)

              window.alert("payment is success")
                router.push('/success')
            }
        }
            )
    }

    return{
        formState,
        renderCard,
        proFeaturesData,
        payment
    }
}
})
</script>
<style scoped>
#card{
    width: 500px;
    margin-left: 400px;
    height: 50px;
    background-color: darkgrey;
}
#error{
    background-color: red;
}
</style>
