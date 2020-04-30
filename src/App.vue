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
              class="-mr-px relative px-4 py-2 border border-gray-300 rounded-l-md text-gray-700 focus:outline-none focus:shadow-outline-blue focus:border-blue-300 z-10">
              <svg fill="none" class="h-5 w-5 text-gray-400" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M13 7a4 4 0 11-8 0 4 4 0 018 0zM9 14a6 6 0 00-6 6v1h12v-1a6 6 0 00-6-6zM21 12h-6" />
              </svg>
            </button>
            <div class="relative flex-grow focus-within:z-20">
              <input id="people" v-model="form.people" class="text-center form-input w-full rounded-none text-sm" placeholder="1" />
            </div>
            <button class="-ml-px relative px-4 py-2 border border-gray-300 rounded-r-md text-gray-700 focus:outline-none focus:shadow-outline-blue focus:border-blue-300">
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
            <input v-model="form.tip" type="checkbox" id="tip" name="tip" checked class="form-checkbox ml-2 h-4 w-4 text-indigo-600 transition duration-150 ease-in-out">
          </div>
        </div>
        <!-- tip -->

        <!-- tip percentage -->
        <div v-show="form.tip" class="w-full md:w-1/2 md:pl-8 mt-5 md:mt-0">
          <span class="w-full relative z-0 inline-flex shadow-sm">
            <button type="button"
              class="relative flex items-center justify-center inline-flex items-center w-1/4 py-2 rounded-l-md border border-gray-300 bg-white text-sm leading-5 font-medium text-gray-700 hover:text-gray-500 focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150">
              5%
            </button>
            <button type="button"
              class="-ml-px relative flex items-center justify-center inline-flex items-center w-1/4 py-2 border border-gray-300 bg-white text-sm leading-5 font-medium text-gray-700 hover:text-gray-500 focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150">
              10%
            </button>
            <button type="button"
              class="-ml-px relative flex items-center justify-center inline-flex items-center w-1/4 py-2 border border-gray-300 bg-white text-sm leading-5 font-medium text-gray-700 hover:text-gray-500 focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150">
              15%
            </button>
            <button type="button"
              class="-ml-px relative flex items-center justify-center inline-flex items-center w-1/4 py-2 rounded-r-md border border-gray-300 bg-white text-sm leading-5 font-medium text-gray-700 hover:text-gray-500 focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150">
              20%
            </button>
          </span>
        </div>
        <!-- tip percentage -->
      </div>
      <!-- tip block-->

      <!-- footer -->
      <div class="mt-8 flex justify-between items-center">
        <span class="text-gray-500 border-b border-gray-500 text-sm leading-snug">Reset</span>
        <span class="inline-flex rounded-md shadow-sm">
          <button type="button"
            class="inline-flex items-center px-4 py-2 border border-transparent text-sm leading-5 font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-500 focus:outline-none focus:border-indigo-700 focus:shadow-outline-indigo active:bg-indigo-700 transition ease-in-out duration-150">
            Calculate
          </button>
        </span>
      </div>
      <!-- footer -->
    </div>

    <!-- results -->
    <div v-if="showResults" class="w-full md:max-w-xl border border-gray-200 bg-white py-4 md:py-6 px-5 md:px-8 text-gray-800 md:rounded-md shadow-md mt-8">
      <!-- Will use justify-between if it has tip, justify-center if not -->
      <div class="mt-5 flex items-center justify-between">
        <!-- pay per person -->
        <div class="w-1/3 flex flex-col items-center">
          <svg class="h-5 w-5 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
          </svg>
          <div class="text-gray-600 flex flex-col items-center">
            <span class="text-gray-600 font-bold text-xl md:text-4xl leading-snug">14€</span>
            <span class="text-sm">each one</span>
          </div>
        </div>
        <!-- pay per person -->

        <span class="text-gray-600 text-2xl">+</span>

        <!-- tip per person -->
        <div class="w-1/3 flex flex-col items-center">
          <svg class="h-5 w-5 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M14.121 15.536c-1.171 1.952-3.07 1.952-4.242 0-1.172-1.953-1.172-5.119 0-7.072 1.171-1.952 3.07-1.952 4.242 0M8 10.5h4m-4 3h4m9-1.5a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>

          <div class="text-gray-600 flex flex-col items-center">
            <span class="text-gray-600 font-bold text-xl md:text-4xl leading-snug">5€</span>
            <span class="text-sm">tip</span>
          </div>
        </div>
        <!-- tip per person -->

        <span class="text-gray-600 text-2xl">=</span>

        <!-- total per person -->
        <div class="w-1/3 flex flex-col items-center">
           <svg class="h-5 w-5 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M14.828 14.828a4 4 0 01-5.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          <div class="text-gray-600 flex flex-col items-center">
            <span class="text-gray-600 font-bold text-xl md:text-4xl leading-snug">19€</span>
            <span class="text-sm">total</span>
          </div>
        </div>
        <!-- total per person -->
      </div>
    </div>
    <!-- results -->
  </div>
</template>
<script>
export default {
  name: "App",

  data() {
    return {
      form: {
        amount: 0,
        people: 1,
        tip: false,
        tipAmount: '',
      },
      showResults: false,
    }
  },
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