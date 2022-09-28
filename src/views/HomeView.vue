<template>
  <div class="p-5 h-screen bg-gray-100">
    <h1 class="text-xl mb-2">Your orders</h1>
    <div class="flex items-center md:order-2">
      <router-link
        class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
        to="/adduser"
        >Add User</router-link
      >
    </div>
    <div class="overflow-auto rounded-lg shadow hidden md:block">
      <table class="w-full">
        <thead class="bg-gray-50 border-b-2 border-gray-200">
          <tr>
            <th
              class="w-20 p-3 text-sm font-semibold tracking-wide text-left"
            ></th>
            <th class="p-3 text-sm font-semibold tracking-wide text-left">
              Name
            </th>
            <th class="w-24 p-3 text-sm font-semibold tracking-wide text-left">
              Website
            </th>
            <th class="w-24 p-3 text-sm font-semibold tracking-wide text-left">
              Phone
            </th>
            <th class="w-24 p-3 text-sm font-semibold tracking-wide text-left">
              Email
            </th>
          </tr>
        </thead>
        <tbody class="divide-y divide-gray-100">
          <tr class="bg-white" v-for="(user, i) in users" :key="`users_${i}`">
            <td class="p-3 text-sm text-gray-700 whitespace-nowrap">
              {{ user.name }}
            </td>
            <td class="p-3 text-sm text-gray-700 whitespace-nowrap">
              {{ user.website }}
            </td>
            <td class="p-3 text-sm text-gray-700 whitespace-nowrap">
              {{ user.phone }}
            </td>
            <td class="p-3 text-sm text-gray-700 whitespace-nowrap">
              {{ user.email }}
            </td>
            <td class="p-3 text-sm text-gray-700 whitespace-nowrap">
              <button
                @click="deleteUser(user.id)"
                class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-4 py-2 md:px-5 md:py-2.5 mr-1 md:mr-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
              >
                DELETE
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 md:hidden">
      <div
        class="bg-white space-y-3 p-4 rounded-lg shadow"
        v-for="(user, i) in users"
        :key="`users_${i}`"
      >
        <div class="flex items-center space-x-2 text-sm">
          <div>
            <div>{{ user.name }}</div>
          </div>
        </div>
        <div class="text-sm text-gray-700">{{ user.phone }}</div>
        <div class="text-sm font-medium text-black">{{ user.email }}</div>
        <div class="text-sm font-medium text-black">
          <button
            @click="deleteUser(user.id)"
            class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-4 py-2 md:px-5 md:py-2.5 mr-1 md:mr-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
          >
            DELETE
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      loading: false,
      users: [],
    };
  },

  mounted() {
    this.loading = true;
    axios
      .get("https://jsonplaceholder.typicode.com/users")
      .then((response) => {
        if (localStorage.getItem("apiData")) {
          this.users = JSON.parse(localStorage.getItem("apiData"));
        } else {
          localStorage.setItem("apiData", JSON.stringify(response.data));
          this.users = JSON.parse(localStorage.getItem("apiData"));
        }
        this.loading = false;
      })
      .catch((e) => {
        console.log("e", e);
        this.loading = false;
      });
  },
  methods: {
    deleteUser(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/users/${id}`)
        .then(() => {
          this.users = this.users.filter((user) => user.id !== id);
          localStorage.setItem("apiData", JSON.stringify(this.users));
        })
        .catch((e) => {
          console.log("e", e);
        });
    },
  },
};
</script>
