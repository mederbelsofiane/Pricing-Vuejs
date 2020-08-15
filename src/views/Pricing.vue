<template>
  <div class="flex justify-center ">
    <div class="w-1/2 bg-blue-900 rounded px-6 py-12 flex flex-col items-center shadow-2xl">
      <div class="flex bg-gray-400 rounded-full justify-around p-1 mb-4">

        <!-- Coder Tape Solution-->
        <button v-for="(price,offer) in plans[0].pricing" v-bind:key="price" class="rounded-full text-xs uppercase px-6 py-1 font-bold focus:outline-none "
                :class="currentOffer===offer ? 'bg-blue-400 text-gray-200':''"
                @click="currentOffer=offer">{{ offer }}</button>



        <!--    MY SOLUTION        <button v-for="offer in offers"
                class="rounded-full text-xs uppercase px-6 py-1 font-bold focus:outline-none"
                :class="currentOffer==offer ? 'bg-blue-400 text-gray-200':''"
                @click="currentOffer=offer">{{offer}}</button>-->

      </div>

      <div class="w-full flex flex-row justify-around pt-4 ">

        <div v-for="plan in plans" v-bind:key="plan.title" class=" w-1/2 bg-blue-300 m-2 p-3 rounded-full">
          <h1 class="text-2xl font-bold pb-2">{{ plan.title }}</h1>
          <ul>
            <li v-for="benefit in plan.benefits[currentOffer]" v-bind:key="benefit">{{benefit}}</li>
          </ul>
          <div class="flex justify-center pt-8">

            <div class="font-bold text-4xl">{{getPrice(plan.pricing[currentOffer].price)}}</div>
            <div class="text-xs font-bold  pt-2 pl-1">{{plan.pricing[currentOffer].label}}</div>

          </div>
        </div>
      </div>
      <div class="pt-4 text-gray-500 text-center text-sm font-bold">
        <a href="#" @click.prevent="currency = 'usd'">USD</a> |
        <a href="#" @click.prevent="currency = 'eur'">EUR</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Pricing",

  methods: {
    getPrice(price){
      return this['currency'+this.currency.toUpperCase()](price)
    },
    currencyUSD(price){
      return '$' + price
    },
    currencyEUR(price){
      return Math.ceil(price *0.85) +'€'
    }
  },

  data: function (){
    return{
      currentOffer:'monthly',
      currency:'usd',
      offers:['monthly','yearly','lifetime'],
      plans:[
        //  first object
        {
          title:'Basic',
          benefits:{
            monthly:['benefit 1','benefit 2','benefit 3'],
            yearly:['benefit 1','benefit 2','benefit 3','benefit 4'],
            lifetime:['benefit 1','benefit 2','benefit 3','benefit 4','benefit 5']
          },
          pricing: {
            monthly:{price:99,label:'/mo'},
            yearly:{price:499,label:'/yr'},
            lifetime:{price:1199,label:''},
          }
        },
        //Seconde object
        {
          title:'Pro',
          benefits:{
            monthly:['benefit 1','benefit 2','benefit 3'],
            yearly:['benefit 1','benefit 2','benefit 3','benefit 4'],
            lifetime:['benefit 1','benefit 2','benefit 3','benefit 4','benefit 5']
          },
          pricing:{
            monthly:{price:149,label:'/mo'},
            yearly:{price:999,label:'/yr'},
            lifetime:{price:2199,label:''},
          }
        }
      ]
    }
  }
}
</script>
