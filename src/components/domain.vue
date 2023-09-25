<template>
  <div class="flex flex-col">
    <h1 class="font-bold text-4xl text-center mb-10">Domain Name</h1>
    <div class="flex justify-center">
      <div class="flex gap-2">
        <input type="text" class="border-1 border-gray-200 p-4 text-black placeholder-zinc-950 rounded-xl outline-0 w-[300px]" placeholder="Domain name" v-model="domain">
        <button @click="submit" class="bg-black text-white rounded-2xl w-[100px] md:w-[90px] transition-all duration-500 hover:bg-orange-400">Whois</button>
      </div>
    </div>
    <hr class="mb-3 mt-3" />
    <div v-if="whoisData">
      <table class="table border-separate border-spacing-2 border border-slate-400">
        <tbody>
        <tr>
          <td><strong>Server:</strong></td>
          <td>{{ whoisData.server }}</td>
        </tr>
        <tr>
          <td><strong>Domain Name:</strong></td>
          <td>{{ whoisData.name }}</td>
        </tr>
        <tr>
          <td><strong>Name Servers:</strong></td>
          <td>{{ whoisData.nameserver }}</td>
        </tr>
        <tr>
          <td><strong>IP:</strong></td>
          <td>{{ whoisData.ips }}</td>
        </tr>
        <tr>
          <td><strong>Created Date:</strong></td>
          <td>{{ whoisData.created }}</td>
        </tr>
        <tr>
          <td><strong>Changed Date:</strong></td>
          <td>{{ whoisData.changed }}</td>
        </tr>
        <tr>
          <td><strong>Expired Date:</strong></td>
          <td>{{ whoisData.expires }}</td>
        </tr>
        <tr>
          <td><strong>Status:</strong></td>
          <td>
            <span v-if="whoisData.registered" class="bg-red-600 text-white p-2 rounded-sm">Purchased</span>
            <span v-else class="bg-green-600 text-white p-2 rounded-sm">Available for Purchase</span>
          </td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script setup>
</script>
<script>
import axios from 'axios';

export default {
  data() {
    return {
      domain: '',
      whoisData: null,
      error : null
    }
  },
  methods: {
    async submit() {
      const options = {
        method: 'GET',
        url: 'https://zozor54-whois-lookup-v1.p.rapidapi.com/',
        params: {
          domain: this.domain,
          format: 'json',
          _forceRefresh: '0'
        },
        headers: {
          'X-RapidAPI-Key': 'f310731f6bmshd0c07ff41a3c723p1972e7jsnc088ba2b61c7',
          'X-RapidAPI-Host': 'zozor54-whois-lookup-v1.p.rapidapi.com'
        }
      };

      try {
        const response = await axios.request(options);
        this.whoisData = response.data
      } catch (error) {
        this.error = error
      }
    }
  }
}
</script>
