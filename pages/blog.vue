<template>
  <main>
    <Navbar />
    <h1>Blog</h1>
    <p v-if="$fetchState.pending">Fetching mountains...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>
    <div v-else>
      <h1>Nuxt Mountains</h1>
      <ul>
        <li v-for="blog of blogs">{{ blog.Title }}</li>
      </ul>
      <button @click="$fetch">Refresh</button>
    </div>
  </main>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      blogs: [],
    };
  },
  async fetch() {
    this.blogs = await fetch(
      "https://cockpit.jaysoft.dev/api/content/item/modelvidu",
      {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          "api-key": "API-ab6b016943b0d74d10fac460e1a6706a7d2718f9",
        },
      }
    ).then((res) => res.json());
  },
};
</script>
