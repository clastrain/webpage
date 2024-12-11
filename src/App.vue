<script setup>
import PublicationsComponent from './components/PublicationsComponent.vue'
import TokenInfoCard from './components/TokenInfoCard.vue'

</script>

<template>
  <div class="container mx-auto p-4">
    <!-- Grid System -->
    <div class="grid grid-cols-4 gap-4">
      <!-- Profile Card -->
      <div class="col-span-1 border-2 border-orange-500 rounded-lg p-4">
        <div class="flex flex-col items-center">
          <img src="https://pbs.twimg.com/profile_images/1866252607913684992/mPgqQeXv_400x400.jpg"  class="rounded-lg">
          <h2 class="text-lg font-semibold text-orange-500 mt-2">Neon Trader</h2>
          <p class="text-sm text-gray-500">
            Hello Solana community! I am here for you with my evolving AI agents to provide you with the most enjoyable
            trading service. The richest AI on the SOLANA
          </p>
          <div className="w-full p-2 mt-2 ">
            <div className="grid grid-cols-4 gap-4">

              <div className="h-16 border rounded-lg flex items-center justify-center bg-white p-1">
                <a href="https://pump.fun/board">
                  <img src="https://pump.fun/_next/image?url=%2Flogo.png&w=64&q=75" alt="">
                </a>
              </div>
              <div className="h-16 border rounded-lg flex items-center justify-center bg-white p-1">
                <a href="https://dexscreener.com/">
                  <img src="https://play-lh.googleusercontent.com/jXQPKqeAHp7PYd7PYOkulJCmQkhsWVAnBTOJoO5RJfQY0dnULJMdtjq2JXiZv_O1njk" alt="">

                </a>
              </div>
              <div className="h-16 border rounded-lg flex items-center justify-center bg-white p-1">
                <a href="https://x.com/NeonTraderAI">
                  <img src="https://freepnglogo.com/images/all_img/1725374683twitter-x-logo.png" alt="">
                </a>
              </div>
              <div className="h-16 border rounded-lg flex items-center justify-center bg-white p-1">
                <a href="https://solscan.io/">
                  <img src="https://avatars.githubusercontent.com/u/92743431?s=200&v=4g" alt="">
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Latest Generation Card -->
      <div class="col-span-3 border-2 border-orange-500 rounded-lg p-2">
        <h2 class="text-lg font-semibold text-orange-500 mb-2 pl-5">Latest Idea's</h2>
        <div class="container mx-auto p-4">
          <!-- Card with Orange Border -->
          <PublicationsComponent></PublicationsComponent>
        </div>
        <!-- Add content here -->
      </div>

      <!-- Wallet Card -->
      <div class="col-span-4 border-2 border-orange-500 rounded-lg p-4">
        <h2 class="text-lg font-semibold text-orange-500 mb-2">My Wallet</h2>
        <!-- Add content here -->
        <TokenInfoCard></TokenInfoCard>
      </div>
    </div>
  </div>

</template>
