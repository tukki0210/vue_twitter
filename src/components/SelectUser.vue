<template>
  <div class="menu">
    <h5 class="text-success">ユーザーの切り替え</h5>
    <select class="form-select" v-model="selectedUser">
      <option
        v-for="tweet_user in tweet_users"
        v-bind:value="tweet_user"
        v-bind:key="tweet_user.user_id"
      >
        {{ tweet_user.user_name }}
      </option>
    </select>
    <button class="text-white bg-primary p-2 m-2 rounded" v-on:click="changeUser">切り替え</button>
  </div>
</template>

<script>
export default {
  name: "SelectUser",
  data() {
    return {
      tweet_users: [
        { user_id: "test_a", user_name: "Aさん" },
        { user_id: "test_b", user_name: "Bさん" },
        { user_id: "test_c", user_name: "Cさん" },
      ],
      selectedUser: { user_id: "test_a", user_name: "Aさん" },
    };
  },
  methods: {
    changeUser(){
      this.$emit('selectUser-event',this.selectedUser)
    }
  },
};
</script>
<style>
.menu {
margin: 5px;
font-size:large;
width: 20%;
margin: 30px;
}
</style>
