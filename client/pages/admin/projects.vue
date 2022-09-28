<template>
  <div>
    <h1 class="text-center text-4xl py-2">Details</h1>
    <p class="text-center" v-if="$fetchState.pending">Loading....</p>
    <p class="text-center" v-else-if="$fetchState.error">Error while fetching mountains</p>
    <div v-else class="flex flex-col justify-around px-5 py-3 bg-white">
      <!-- <img class="w-10 nth-child(even):text-500" :src=fund.image alt="image"/> -->
      <p><b>AMC code:</b> {{ fund.AMC_code }}</p>
      <p><b>AMC name:</b> {{ fund.amc_name }}</p>
      <p><b>Address:</b> {{ fund.address }}</p>
      <p><b>Description:</b> {{ fund.description}}</p>
      <p><b>Rta info:</b> {{ fund.rta_info }}</p>
      <p><b>Short code:</b> {{ fund.short_code }}</p>
      <p><b>Url:</b> {{ fund.login_url}}</p>
      <p><b>Phone Number:</b> {{ fund.phone_number}}</p>
      <p><b>Website:</b> {{ fund.website}}</p>

    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      id: '',
      fund: {},
      // image: '',
    }
  },
  mounted() {
    console.log("hello", this.$route)
  },
  created() {
    this.id = this.$route.params.id;
  },
  async fetch() {
    const data = await fetch(`https://equirus-tech-backend.vercel.app/funds/${this.id}`).then(res => res.json());
    console.log(data.data);
    this.fund = data.data
    // this.image = data.data.image
  }

}
</script>
