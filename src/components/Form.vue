<template>
  <div class="form form-group">
    <textarea
      name="form"
      id=""
      class="form-control"
      cols="60"
      rows="5"
      placeholder="いまなにしてる？"
      v-model="TweetObj.tweet_body"
    ></textarea>
    <br />
    <button class="text-white bg-success p-2 rounded" v-on:click="doTweet">
      ツイートする
    </button>
  </div>
</template>

<script>
export default {
  name: "Form",
  data() {
    return {
      TweetObj: {
        tweet_id: 0,
        tweet_user: {
          user_id: "TestId",
          user_name: "ユーザー",
        },
        tweet_body: "",
      },
    };
  },
  methods: {
    doTweet() {
      this.TweetObj.tweet_id += 1;

      // 値渡しするために、新しいオブジェクトを定義する
      const tweet = Object.assign({}, this.TweetObj);
      this.$emit("tweet-event", tweet);
    },
  },
};
</script>
