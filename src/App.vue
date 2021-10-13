<template>
<div>
   <HelloWorld />
  <div class="wrapper">
    <div class="menu">
      <p class="text-success">ユーザーの切り替え</p>
      <ul class="list-group">
        <li class="list-group-item" v-on:click="chengeUser"></li>
      </ul>

    </div>
    <div class="tweet-contents">
      <h2 class="text-success">Twitter-Vue3</h2>
      <div class="content">
        <Form v-on:tweet-event="tweetAction" />
        <div style="margin-top:20px">
          <Tweet
            v-for="Tweet in AllTweet"
            v-bind:TweetObj="Tweet"
            v-bind:key="Tweet.tweet_id"
          />
        </div>
      </div>
    </div>
   
  </div>
  </div>
</template>

<script>
import Form from "./components/Form.vue";
import Tweet from "./components/Tweet.vue";

import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    Form,
    Tweet,
    HelloWorld,
  },
  data() {
    return {
      AllTweet: Array.of({
        tweet_id: 0,
        tweet_user: {
          user_id: "TestId",
          user_name: "ユーザー",
        },
        tweet_body: "はじめてのツイート",
      }),
    };
  },
  methods: {
    tweetAction(TweetObj) {
      this.AllTweet.push(TweetObj);
      localStorage.setItem(TweetObj.tweet_id,TweetObj);
      console.log(localStorage);
    },
    changeUser(){
      console.log('A')
    }
  },
};
</script>
<style>
.wrapper {
  display: flex;
  margin: 20px auto;
}
.menu {
  width: 20%;
  margin: 30px;
  border:1px solid green;
}
.tweet-content {
  width: 60%;
}
.content {
  margin: 20px auto;
  width: 100%;
}
</style>
