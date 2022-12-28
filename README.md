<createCustomer 
@customer-createsuccess="customerCreationSuccess" 
@create-customerfail="customerCreationFail"

/>
<Subscription  
  @subscription-fail="subscriptionCreationFail" 
  @subscription-success="subscriptionCreationSuccess"
  />
  
<Checkout
@payment-Fail="paymentFail" 
@payment-success="paymentSuccess" 
/>




emitted methods 

@customerCreatesuccess will be emitted when customer is created and customerId is obtained 

@create-customerfai will be emitted when error occured while customer creation and error will returned
  
@subscription-success will be emitted when customer is created and clientSecret is obtained is obtained 
  
@subscription-fail will be emitted when error occured while subscription creation and error will returned
  
@paymentSuccess  will be emitted when payment is success  and payment object returned

@payment-Fail will be emitted when payment is failed  and error object returned



@Stripe ApiKeys
Update stripe publicKey in src/components/checkoutComponent.vue
Update stripe secretKey in backend/routes/api/post.js

