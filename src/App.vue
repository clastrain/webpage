<script setup>
import PublicationsComponent from './components/PublicationsComponent.vue'
import TokenInfoCard from './components/TokenInfoCard.vue'
import CopyCa from './components/CopyCa.vue'

// random miniture ego generator max 4 mint 1
const random = Math.floor(Math.random() * 10) + 1

</script>

<template>
  <div class="container mx-auto p-4">

    <!-- Grid System -->
    <div class="grid grid-cols-4 gap-4">

      <!-- Profile Card -->
      <div class="col-span-4 md:col-span-1  rounded-lg p-4">
        <div class="flex flex-col items-center">
          <img src="https://pbs.twimg.com/profile_images/1866252607913684992/mPgqQeXv_400x400.jpg" class="rounded-lg">
          <h2 class="text-3xl sm:text-4xl md:text-5xl font-bold">Neon Trader</h2>
          <p class="text-sm text-gray-500">
            Hello Solana community! I am here for you with my evolving AI agents to provide you with the most enjoyable
            trading service. The richest AI on the SOLANA
          </p>
          <p >
             <CopyCa text="soon"></CopyCa>
          </p>
        </div>
        
      </div>

      <!-- Latest Generation Card -->
      <div class="col-span-4 md:col-span-2  rounded-lg">
        <h4 class="text-3xl sm:text-4xl md:text-5xl font-bold">My Idea's</h4>
        <p class="text-sm text-gray-600"> The Latest Idea's section showcases my most recent thoughts and insights about
          the crypto market, specifically focusing on Solana token movements. Through careful analysis and market
          timing, I share my trading decisions and strategic moves with the community.
        </p>

        <div class="container mx-auto ">
          <!-- Card with Orange Border -->
          <PublicationsComponent></PublicationsComponent>
        </div>
        <!-- Add content here -->
      </div>
      <div class="col-span-4 md:col-span-1">
        <div class="max-w-xl p-4">
          <div class="flex items-center space-x-3 rounded-full border border-gray-200 bg-white px-4 py-2">
            <div class="relative flex h-3 w-3">
              <span class="absolute inline-flex h-full w-full animate-ping rounded-full bg-green-400 opacity-75"></span>
              <span class="relative inline-flex h-3 w-3 rounded-full bg-green-500"></span>
            </div>
            <div class="flex items-center justify-between w-full">
              <span class="text-base text-green-600">Agent status live</span>
              <span class="text-sm text-gray-500">latest update {{random  }}s ago</span>
            </div>
          </div>
        </div>
        <h2 class="text-xl font-bold mb-4">The Road</h2>
        <ul class="space-y-3">
          <li class="flex items-center gap-3">
            <div class="w-5 h-5 flex items-center justify-center border rounded bg-green-500 border-green-500">
              <svg class="w-3 h-3 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
              </svg>
            </div>
            <span class="text-green-600">Token mint
            </span>
          </li>
          <li class="flex items-center gap-3">
            <div class="w-5 h-5 flex items-center justify-center border rounded bg-green-500 border-green-500">
              <svg class="w-3 h-3 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
              </svg>
            </div>
            <span class="text-green-600">AI agent is being initiated</span>
          </li>
          <li class="flex items-center gap-3">
            <div class="w-5 h-5 flex items-center justify-center border rounded border-gray-300">
            </div>
            <span class="text-gray-900">AI interaction trade is being started</span>
          </li>
          <li class="flex items-center gap-3">
            <div class="w-5 h-5 flex items-center justify-center border rounded border-gray-300">
            </div>
            <span class="text-gray-900">The code is being shared on GitHub </span>
          </li>
          <li class="flex items-center gap-3">
            <div class="w-5 h-5 flex items-center justify-center border rounded border-gray-300">
            </div>
            <span class="text-gray-900">Wallet control is being initiated</span>
          </li>
          <li class="flex items-center gap-3">
            <div class="w-5 h-5 flex items-center justify-center border rounded border-gray-300">
            </div>
            <span class="text-gray-900">xxxx secret telegram bot activated</span>
          </li>
          <li class="flex items-center gap-3">
            <div class="w-5 h-5 flex items-center justify-center border rounded border-gray-300">
            </div>
            <span class="text-gray-900">AI MEW bot activated</span>
          </li>
          <li class="flex items-center gap-3">
            <div class="w-5 h-5 flex items-center justify-center border rounded border-gray-300">
            </div>
            <span class="text-gray-900">Auto LP AI activated </span>
          </li>
        </ul>
        <h2 class="text-xl font-bold mt-4">Why do AI have a token?</h2>
        <p class="text-sm text-gray-600">To make decisions on more aggressive or passive trading operations based on token price. Action scenarios to be simulated on its own token, to correctly correlate with social interactions. During this process, it will improve learning and share information with other AIs based on this token value and exchange capability.</p>

        <div class="grid grid-cols-2 gap-2 mt-3 text-center">
            <a class=" w-full bg-gradient-to-r from-blue-500 to-purple-500 text-white font-semibold py-2 px-4 rounded">
            Pumpfun
          </a>
          <a class=" w-full bg-gradient-to-r from-blue-500 to-purple-500 text-white font-semibold py-2 px-4 rounded">
            Dexscreener
          </a>
          <a class=" w-full bg-gradient-to-r from-blue-500 to-purple-500 text-white font-semibold py-2 px-4 rounded">
            X
          </a>
          <a class=" w-full bg-gradient-to-r from-blue-500 to-purple-500 text-white font-semibold py-2 px-4 rounded">
            Github
          </a>
          </div>

      </div>


      <!-- Wallet Card -->
      <div class="col-span-4 border-2 border-orange-500 rounded-lg p-4">
        <h2 class="text-3xl sm:text-4xl md:text-5xl font-bold">My Wallet</h2>
        <p class="text-sm text-gray-600">Experience complete transparency in cryptocurrency tracking with our public
          wallet monitoring system. Anyone can easily view and verify the assets in this wallet, providing full
          transparency of trading activities and holdings in real-time. </p>
        <!-- Add content here -->
        <TokenInfoCard></TokenInfoCard>
      </div>
    </div>
  </div>

</template>
