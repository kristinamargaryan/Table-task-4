<template>
  <nav class="bg-white border-gray-200 px-2 md:px-4 py-2.5 dark:bg-gray-900">
    <div
      class="flex flex-wrap justify-between items-center mx-auto max-w-screen-xl"
    >
      <div class="flex items-center">
        <img
          src="https://flowbite.com/docs/images/logo.svg"
          class="mr-3 h-6 sm:h-9"
          alt="Flowbite Logo"
        />
        <router-link
          class="self-center text-xl font-semibold whitespace-nowrap dark:text-white"
          to="/"
          >Home</router-link
        >
      </div>

      <div
        id="mega-menu"
        class="hidden justify-between items-center w-full text-sm md:flex md:w-auto md:order-1"
      ></div>
    </div>
  </nav>

  <router-view />
</template>

<style lang="scss"></style>
