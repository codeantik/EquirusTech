<template>
  <!-- <Content /> -->
  <!-- <h1>hello</h1> -->
  <p v-if="$fetchState.pending">Loading....</p>
  <p v-else-if="$fetchState.error">Error while fetching mountains</p>
  <ul v-else class="flex flex-col bg-white">
    <li v-for="(item, index) in funds" :key="index">
      <div class="flex flex-row py-7 px-5 justify-between items-center">
        <!-- <h1>{{ item[0] }}</h1> -->
        <p>{{item[1][0].c}}</p>
        <p>{{item[1][0].kc}}</p>
        <p>{{item[1][0].n}}</p>
        <p>{{item[1][0].re}}</p>
        <p>{{item[1][0].v}}</p>
        <button class="p-2 text-blue-500 border-blue-500 border-2 rounded-sm cursor-pointer hover:bg-blue-500 hover:text-white" @click="goToDetails(item[0])">View More</button>
        <!-- <router-link :to="{ name: 'admin-projects', params: { id: item[0] } }">Navigate to Page2</router-link> -->
      </div>
    </li>
  </ul>

</template>

<script>
// import Content from '../components/Content.vue'

// export default {
//   components: {
//     Content,
//   },
// }

  export default {
    data() {
      return {
        funds: {
        },
      }
    },
    async fetch() {
      const data = await fetch(`https://equirus-server.vercel.app/funds`).then(res => res.json());
      // console.log(data.data.Debt);
      const response = Object.entries(Object.values(data.data.Debt)[0])
      // console.log(Object.entries(Object.entries(data.data.Debt)[1]))
      this.funds = response;
      console.log(this.funds);
    },
    fetchOnServer: false,
    methods: {
      goToDetails(name) {
        console.log(name)
        this.$router.push({ name: 'admin-projects', params: { id: name }})
        // this.$router.push('/admin/projects')
      }
    }
  }
  

</script>
