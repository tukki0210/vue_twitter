<template>
    <div ref="ans" v-on:click="doAction">{{ans}}</div>
</template>

<script>
export default {
    name: "Ans",
    props:{
        ans:String
    },
    // data(){

    // },
    methods: {
        doAction(){
            if (this.ans === "北岳"){
            this.$refs.ans.innerHTML = "正解";
            }
        }
    },
}
</script>