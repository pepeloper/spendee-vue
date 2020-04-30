<template>
  <div class="min-h-screen w-full flex flex-col items-center justify-between md:justify-start background">
    <div class="mt-0 md:mt-48 w-full md:max-w-xl border border-gray-200 bg-white py-4 md:py-6 px-5 md:px-8 text-gray-800 md:rounded-md md:shadow-md">
      <!-- card header -->
      <div class="flex justify-between items-center">
        <h1 class="text-3xl text-gray-800">💸 Spendee</h1>
      </div>
      <!-- card header -->

      <!-- total amount & people -->
      <div class="mt-5 w-full flex flex-col md:flex-row justify-between border-b border-dotted pb-6 border-gray-400">
        <!-- total amount -->
        <div class="w-full md:w-1/2 md:pr-8">
          <label for="amount" class="block text-sm font-medium text-gray-700">Amount to pay</label>
          <div class="mt-1 relative rounded-md shadow-sm">
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
              <span class="text-gray-500 sm:text-sm">
                $
              </span>
            </div>
            <input v-model="form.amount" id="amount" class="form-input w-full pl-8 pr-12 sm:text-sm" placeholder="0.00"
              aria-describedby="price-currency" />
            <div class="absolute inset-y-0 right-0 pr-3 flex items-center pointer-events-none">
              <span class="text-gray-500 sm:text-sm" id="price-currency">
                EUR
              </span>
            </div>
          </div>
        </div>
        <!-- total amount -->

        <!-- people -->
        <div class="w-full md:w-1/2 md:pl-8 mt-5 md:mt-0">
          <label for="people" class="block text-sm font-medium text-gray-700">People</label>
          <div class="mt-1 flex rounded-md shadow-sm">
            <button
              @click="removePerson"
              class="-mr-px relative px-4 py-2 border border-gray-300 rounded-l-md text-gray-700 focus:outline-none focus:shadow-outline-blue focus:border-blue-300 z-10"
            >
              <svg fill="none" class="h-5 w-5 text-gray-400" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M13 7a4 4 0 11-8 0 4 4 0 018 0zM9 14a6 6 0 00-6 6v1h12v-1a6 6 0 00-6-6zM21 12h-6" />
              </svg>
            </button>
            <div class="relative flex-grow focus-within:z-20">
              <input id="people" v-model="form.people" class="text-center form-input w-full rounded-none text-sm" placeholder="1" />
            </div>
            <button
              @click="addPerson"
              class="-ml-px relative px-4 py-2 border border-gray-300 rounded-r-md text-gray-700 focus:outline-none focus:shadow-outline-blue focus:border-blue-300"
            >
              <svg class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M18 9v3m0 0v3m0-3h3m-3 0h-3m-2-5a4 4 0 11-8 0 4 4 0 018 0zM3 20a6 6 0 0112 0v1H3v-1z" />
              </svg>
            </button>
          </div>
        </div>
        <!-- people -->
      </div>
      <!-- total amount & people -->

      <!-- tip block-->
      <div class="mt-5 flex flex-col md:flex-row items-center justify-between h-auto md:h-8">
        <!-- tip -->
        <div class="w-full md:w-1/2 md:pr-8">
          <div class="flex items-center justify-center md:justify-start">
            <label class="inline-block text-sm font-medium text-gray-700" for="tip">Do you want to tip?</label>
            <input v-model="form.tip" type="checkbox" id="tip" name="tip" class="form-checkbox ml-2 h-4 w-4 text-indigo-600 transition duration-150 ease-in-out">
          </div>
        </div>
        <!-- tip -->

        <!-- tip percentage -->
        <div v-show="form.tip" class="w-full md:w-1/2 md:pl-8 mt-5 md:mt-0">
          <span class="w-full relative z-0 inline-flex">
            <button
              type="button"
              v-for="(tip, index) in tipOptions"
              :key="tip.value"
              class="relative flex items-center justify-center inline-flex items-center w-1/4 py-2 border border-gray-300 bg-white text-sm leading-5 font-medium text-gray-700 hover:text-gray-500 focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150"
              :class="{ 'rounded-l-md': index === 0, 'rounded-r-md': index === tipOptions.length - 1, '-ml-px': index > 0 }"
              @click="setTipPercentage(tip.value)"
            >
              {{ tip.label }}
            </button>
          </span>
        </div>
        <!-- tip percentage -->
      </div>
      <!-- tip block-->

      <!-- footer -->
      <div class="mt-8 flex justify-between items-center">
        <span @click="resetForm" class="text-gray-500 border-b border-gray-500 text-sm leading-snug">Reset</span>
        <span class="inline-flex rounded-md shadow-sm">
          <button
            @click="calculate"
            type="button"
            class="inline-flex items-center px-4 py-2 border border-transparent text-sm leading-5 font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-500 focus:outline-none focus:border-indigo-700 focus:shadow-outline-indigo active:bg-indigo-700 transition ease-in-out duration-150"
          >
            Calculate
          </button>
        </span>
      </div>
      <!-- footer -->
    </div>

    <ResultCard v-if="showResults" :bill="form" />
  </div>
</template>

<script>
import ResultCard from './components/ResultCard'

export default {
  name: "App",

  components: {
    ResultCard,
  },

  data() {
    return {
      form: {
        amount: 0,
        people: 1,
        tip: false,
        tipAmount: null,
      },
      showResults: false,
      tipOptions: [
        { label: '5%', value: '5' },
        { label: '10%', value: '10' },
        { label: '15%', value: '15' },
        { label: '20%', value: '20' },
      ]
    }
  },

  methods: {
    removePerson() {
      if (this.form.people > 1) {
        this.form.people--
      }
    },

    addPerson() {
      this.form.people++
    },

    setTipPercentage(percentage) {
      this.form.tipAmount = percentage
    },

    resetForm() {
      this.form.amount = 0
      this.form.people = 1
      this.form.tip = false
      this.form.tipAmount = null
      this.showResults = false
    },

    calculate() {
      this.showResults = true
    },
  }
};
</script>
<style>
  .background {
    background: white;
  }
  @media (min-width: 768px) {
    .background {
      background: url(/assets/images/background.jpeg);
    }
  }
</style>