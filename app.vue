<template>
  <div class="container mx-auto px-4 py-8">
    <h1 class="text-3xl font-bold mb-4">Random User Data</h1>
    <button @click="fetchRandomUser" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
       Random User Data
    </button>

    <div v-if="user" class="mt-4 border border-gray-300 p-4 rounded">
      <div class="flex flex-col space-y-2">
        <label class="font-bold">Name:</label>
        <p>{{ user.name.first }} {{ user.name.last }}</p>
      </div>
      <div class="flex flex-col space-y-2">
        <label class="font-bold">Gender:</label>
        <p>{{ user.gender }}</p>
      </div>
      <div class="flex flex-col space-y-2">
        <label class="font-bold">Email:</label>
        <p>{{ user.email }}</p>
      </div>
      <div class="flex flex-col space-y-2">
        <label class="font-bold">Date of Birth:</label>
        <p>{{ user.dob.date }}</p>
      </div>
      <div class="flex flex-col space-y-2">
        <label class="font-bold">Phone:</label>
        <p>{{ user.phone }}</p>
      </div>
      <img :src="user.picture.large" :alt="user.name.first + ' ' + user.name.last" class="mt-4 rounded">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: null
    };
  },
  methods: {
    async fetchRandomUser() {
      try {
        const response = await fetch("https://randomuser.me/api/");
        if (!response.ok) {
          throw new Error("Failed to fetch random user");
        }
        const data = await response.json();
        this.user = data.results[0];
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>


<style>
button {
  text-decoration: none;
  position: relative;
  border: none;
  font-size: 14px;
  font-family: inherit;
  cursor: pointer;
  color: #fff;
  width: 9em;
  height: 3em;
  line-height: 2em;
  text-align: center;
  background: linear-gradient(90deg, #03a9f4, #f441a5, #ffeb3b, #03a9f4);
  background-size: 300%;
  border-radius: 30px;
  z-index: 1;
}

button:hover {
  animation: ani 8s linear infinite;
  border: none;
}

@keyframes ani {
  0% {
    background-position: 0%;
  }

  100% {
    background-position: 400%;
  }
}

button:before {
  content: "";
  position: absolute;
  top: -5px;
  left: -5px;
  right: -5px;
  bottom: -5px;
  z-index: -1;
  background: linear-gradient(90deg, #03a9f4, #f441a5, #ffeb3b, #03a9f4);
  background-size: 400%;
  border-radius: 35px;
  transition: 1s;
}

button:hover::before {
  filter: blur(20px);
}

button:active {
  background: linear-gradient(32deg, #03a9f4, #f441a5, #ffeb3b, #03a9f4);
}
</style>
