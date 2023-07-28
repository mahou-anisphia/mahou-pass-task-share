<template>
  <div class="container">
    <input v-model="strStatus" type="text" placeholder="Enter your post" />
    <button @click="add(strStatus)">Post</button>
    <ul>
      <li v-for="(post, index) in statPosts" :key="index">
        {{ post }}
        <button @click="remove(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "AddRequest",
  data() {
    return {
      statPosts: [],
      strStatus: "",
    };
  },
  methods: {
    add(status) {
      if (status.trim() !== "") {
        this.statPosts.push(status);
        this.strStatus = "";
      }
    },
    remove(index) {
      this.statPosts.splice(index, 1);
    },
  },
};
</script>
<style>
ul {
  list-style-type: none;
}
</style>
