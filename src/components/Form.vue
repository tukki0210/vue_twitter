<template>
  <div class="form form-group">
    <textarea
      name="form"
      id=""
      class="form-control"
      cols="60"
      rows="5"
      placeholder="いまなにしてる？"
      v-model="data.TweetObj.tweet_body"
    ></textarea>
    <br />
    <button class="text-white bg-success p-2 m-2 rounded" v-on:click="doTweet">
      ツイートする
    </button>
    <button
      class="text-white bg-secondary p-2 m-2 rounded"
      v-on:click="doReload"
    >
      画面を更新する
    </button>
    <button
      class="text-white bg-danger p-2 m-2 rounded"
      v-on:click="removeAllTweet"
    >
      全ツイートを削除する
    </button>
  </div>
</template>

<script>
import { reactive } from "@vue/reactivity";

export default {
  name: "Form",
  props: {
    user: Object,
  },
  setup(props, context) {
    const data = reactive({
      TweetObj: {
        tweet_id: 0,
        tweet_user: {
          user_id: "TestId",
          user_name: "ユーザー",
        },
        tweet_body: "",
      },
    });

    const doTweet = () => {
      data.TweetObj.tweet_user = props.user;
      console.log(props.user);
      data.TweetObj.tweet_id += 1;
      localStorage.setItem("last_id", JSON.stringify(data.TweetObj.tweet_id));
      // 値渡しするために、新しいオブジェクトを定義する
      const tweet = Object.assign({}, data.TweetObj);
      context.emit("tweet-event", tweet);
    };

    const doReload = () => {
      location.reload();
    };

    const removeAllTweet = () => {
      localStorage.clear();
      location.reload();
    };

    data.TweetObj.tweet_id = Number(localStorage.getItem("last_id"));

    return {
      data,
      doTweet,
      doReload,
      removeAllTweet,
    };
  },
};
</script>
