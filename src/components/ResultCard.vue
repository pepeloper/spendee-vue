<template>
  <div class="w-full md:max-w-xl border border-gray-200 bg-white py-4 md:py-6 px-5 md:px-8 text-gray-800 md:rounded-md shadow-md mt-8">
      <div class="mt-5 flex items-center" :class="{ 'justify-between': hasTip, 'justify-center': !hasTip }">
        <!-- pay per person -->
        <div class="w-1/3 flex flex-col items-center">
          <svg class="h-5 w-5 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
          </svg>
          <div class="text-gray-600 flex flex-col items-center">
            <span class="text-gray-600 font-bold text-xl md:text-4xl leading-snug">{{ toPayEachOne }}€</span>
            <span class="text-sm">each one</span>
          </div>
        </div>
        <!-- pay per person -->

        <span v-if="hasTip" class="text-gray-600 text-2xl">+</span>

        <!-- tip per person -->
        <div v-if="hasTip" class="w-1/3 flex flex-col items-center">
          <svg class="h-5 w-5 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M14.121 15.536c-1.171 1.952-3.07 1.952-4.242 0-1.172-1.953-1.172-5.119 0-7.072 1.171-1.952 3.07-1.952 4.242 0M8 10.5h4m-4 3h4m9-1.5a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>

          <div class="text-gray-600 flex flex-col items-center">
            <span class="text-gray-600 font-bold text-xl md:text-4xl leading-snug">{{ toTipEachOne }}€</span>
            <span class="text-sm">tip</span>
          </div>
        </div>
        <!-- tip per person -->

        <span v-if="hasTip" class="text-gray-600 text-2xl">=</span>

        <!-- total per person -->
        <div v-if="hasTip" class="w-1/3 flex flex-col items-center">
           <svg class="h-5 w-5 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M14.828 14.828a4 4 0 01-5.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          <div class="text-gray-600 flex flex-col items-center">
            <span class="text-gray-600 font-bold text-xl md:text-4xl leading-snug">{{ totalToPay }}€</span>
            <span class="text-sm">total</span>
          </div>
        </div>
        <!-- total per person -->
      </div>
    </div>
</template>
<script>
import currency from 'currency.js'

export default {
  name: 'ResultCard',

  props: {
    bill: {
      type: Object,
      default: () => ({}),
    },
  },

  computed: {
    hasTip() {
      return this.bill.tip
    },

    toPayEachOne() {
      const [ toPay ] = currency(this.bill.amount).distribute(this.bill.people)
      return toPay.value
    },

    totalTip() {
      return (this.bill.tipAmount / 100 ) * Number(this.bill.amount)
    },

    toTipEachOne() {
      const [ toTip ] = currency(this.totalTip).distribute(this.bill.people)
      return toTip.value
    },

    totalToPay() {
      return currency(this.toPayEachOne).add(this.toTipEachOne).value
    }
  },
}
</script>