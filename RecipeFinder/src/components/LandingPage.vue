<template>
  <section class="relative flex items-center justify-center overflow-hidden text-white overscroll-none">
      <img src="@/assets/ingredientsheader.webp" alt="Ingredients" class="absolute inset-0 w-full h-full object-cover">
      <div class="relative p-8 text-center">
          <h1 class="mb-4 text-4xl font-extrabold tracking-tight leading-none text-white md:text-5xl lg:text-6xl">Welcome!</h1>
          <p class="mb-8 text-lg font-normal text-gray-300 lg:text-xl sm:px-16 lg:px-48">Can't quite figure out what to make with what you have? Enter your ingredients, and we'll give you some ideas!</p>
          <div class="flex flex-col lg:space-x-5 md:space-x-3 space-y-4 sm:flex-row sm:justify-center sm:space-y-0 sm:space-x-0">
              <router-link to="/search" class="inline-flex justify-center items-center py-3 px-5 text-lg font-semibold text-center text-white rounded-lg bg-green-700 hover:bg-yellow-700 focus:ring-4 focus:ring-white-300 dark:focus:ring-white-900">
                  Search for Recipes
                  <svg class="w-3.5 h-3.5 ms-2 rtl:rotate-180" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 10">
                      <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 5h12m0 0L9 1m4 4L9 9"/>
                  </svg>
              </router-link>
              <router-link to="/about" class="inline-flex justify-center items-center py-3 px-5 text-lg font-semibold text-center text-white rounded-lg bg-green-700 hover:bg-yellow-700 focus:ring-4 focus:ring-white-300 dark:focus:ring-white-900">
                  Learn more
              </router-link>  
          </div>
      </div>
  </section>
</template>


<style scoped>
section{
  border-radius: 10px;
  border: solid .15rem #ffffff;
  width: 100vw;
  margin-top: 7em;
  box-shadow: 0 0 15px 10px #ffffff;
  max-width: 500px;
  overflow: hidden;
}

p{
  background: #ffffffb3;
  color: black;
  font-weight: 700;
  box-shadow: 0 0 10px 7px #ffffffb3;
  border-radius: 10px;
  padding: .5em;
  text-shadow: 2px 2px 2px #ffffff;
}

h1 {
  text-shadow: 2px 2px 2px #000;
}

@media (max-width: 470px) {
  section{
  border-radius: 10px;
  border: solid .15rem #ffffff;
  width: 90vw;
  margin-top: 7em;
  box-shadow: 0 0 15px 10px #ffffff;
  position: fixed;
  height: 100vw;
}
}
 

</style>