<template>
  <div>
    <form @submit="AddUser" class="my-form">
      <div class="grid gap-6 mb-6 md:grid-cols-2">
        <div>
          <label
            for="name"
            class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
            >First name</label
          >

          <input
            v-bind:value="name"
            @input="name = $event.target.value"
            type="text"
            id="name"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="Name"
            required
          />
        </div>
        <div>
          <label
            for="website"
            class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
            >Website URL</label
          >
          <input
            v-bind:value="website"
            @input="website = $event.target.value"
            type="url"
            id="website"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="flowbite.com"
            required
          />
        </div>
      </div>
      <div class="mb-6">
        <label
          for="phone"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
          >Phone number</label
        >
        <input
          v-bind:value="phone"
          @input="phone = $event.target.value"
          type="tel"
          id="phone"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="123-45-678"
          required
        />
      </div>
      <div class="mb-6">
        <label
          for="email"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
          >Email address</label
        >
        <input
          v-bind:value="email"
          @input="email = $event.target.value"
          type="email"
          id="email"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="email.doe@company.com"
          required
        />
      </div>

      <router-link
        to="/"
        class="text-white bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-blue-300 dark:focus:ring-blue-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2"
      >
        Cancel
      </router-link>
      <button
        @click="AddUser"
        type="submit"
        class="text-white bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-blue-300 dark:focus:ring-blue-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2"
      >
        Submit
      </button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      name: "",
      website: "",
      email: "",
      phone: "",
    };
  },
  methods: {
    AddUser(event) {
      event.preventDefault();
      let newPost = [];
      newPost.push({
        id: Date.now(),
        name: this.name,
        website: this.website,
        email: this.email,
        phone: this.phone,
      });
      axios
        .post("https://jsonplaceholder.typicode.com/users", newPost)
        .then((response) => {
          let data = JSON.parse(localStorage.getItem("apiData"));
          data.push(response.data["0"]);
          localStorage.setItem("apiData", JSON.stringify(data));
        })
        .catch((e) => {
          console.log("e", e);
        })
        .finally(() => {
          this.$router.push("/");
        });
    },
  },
};
</script>

<style lang="scss" scoped>
.my-form {
  margin: 10px;
  padding: 10px;
}
</style>
