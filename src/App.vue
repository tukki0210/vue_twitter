<template>
  <div>
    <HelloWorld title="Composition API" msg="This is Composition API sample" />
    <div class="wrapper">
      <SelectUser v-on:selectUser-event="selectUser" />
      <div class="tweet-contents">
        <h2 class="text-success">Twitter-Vue3</h2>
        <div class="content">
          <Form v-on:tweet-event="tweetAction" v-bind:user="data.tweet_user" />
          <div style="margin-top: 20px">
            <Tweet
              v-for="Tweet in data.AllTweet"
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
import SelectUser from "./components/SelectUser.vue";
import HelloWorld from "./components/HelloWorld.vue";
import { reactive } from '@vue/reactivity';

export default {
  name: "App",
  components: {
    Form,
    Tweet,
    SelectUser,
    HelloWorld
  },
  setup(){
    const data = reactive({
      AllTweet: Array.of({
        tweet_id: 0,
        tweet_user: {
          user_id: "TestId",
          user_name: "ユーザー",
        },
        tweet_body: "はじめてのツイート",
      }),
      tweet_user: {
        user_id: "TestId",
        user_name: "ユーザー",
      },
    })

    const tweetAction = (TweetObj) => {
      data.AllTweet.push(TweetObj);
      localStorage.setItem(
        JSON.stringify(TweetObj.tweet_id),
        JSON.stringify(TweetObj)
      );
      console.log(localStorage)
    }

    const selectUser = (user) => {
      console.log(user)
      data.tweet_user = user;
    }

    for (let i = 1; i < parseInt(localStorage.getItem("last_id")) + 1; i++) {
      data.AllTweet.push(JSON.parse(localStorage.getItem(i)));
    }

    return {
      data,
      tweetAction,
      selectUser
    }
  },
};
</script>
<style>
.wrapper {
  display: flex;
  margin: 20px auto;
}

.tweet-content {
  width: 60%;
}
.content {
  margin: 20px auto;
  width: 100%;
}
</style>
