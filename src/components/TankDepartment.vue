<template>
    <div id="tank-department">
        <div class="title">{{ title }}</div>
        <content-handler :contentNum="0" @next-page="nextPage"></content-handler>
    </div>
</template>

<script>
import ContentHandler from "@/components/ContentHandler";
import json from "../../text.json";
export default {
    name: "tank-department",
    components:
    {
        ContentHandler
    },
    props:[],
    data() {
        return {
            pageNum: 3,
        }
    },
    methods: {
        nextPage() {
            this.$emit('next-page');
        }
    },
    computed: {
        title() { 
            return json.info[this.pageNum].title;
        }
    }
}
</script>

<style scoped>
    @font-face {
        font-family: "aduma";
        src: url("../assets/fonts/Aduma Regular.ttf");
    }
    #tank-department {
        margin: 0%;
        height: 100%;
        width: 100vw;
        position: absolute;
        top: 0;
        right: 0;
    }
    .title {
        text-align: center;
        width: 90vw;
        margin: auto;
        color: #ffc300;
        margin-top: 30%;
        font-family: "aduma";
        font-size: 12vw;
        font-weight: bold;
    }

</style>