<template>
    <div id="discovery">
        <div id="main-title">טכניקות לחימה ממרחב עמדות</div>
        <div id="sub-title">{{ title }}</div>
        <div id="text">{{ explenation }}</div>
        <div id="sub-title2">{{ subTitle }}</div>
        <content-handler :contentNum="1" @next-page="nextPage"></content-handler>
    </div>
</template>

<script>
import ContentHandler from "@/components/ContentHandler";
import json from "../../text.json";
export default {
    name: "discovery",
    components:
    {
        ContentHandler
    },
    props: ["pageNum", "contentNum"],
    data() {
        return {

        }
    },
    methods: {
        nextPage() {
            this.$emit('back-to-menu');
        }
    },
    computed: {
        explenation(){
            return json.info[this.pageNum][this.contentNum-1].explenation;
        },
        subTitle(){
            return json.info[this.pageNum][this.contentNum-1].subTitle;
        },
        title() { 
            return json.info[this.pageNum][this.contentNum-1].title;
        }
    }
}

</script>

<style scoped>
    #discovery {
        margin: 0%;
        height: 100%;
        width: 100vw;
        position: absolute;
        top: 0;
        right: 0;
    }
    #text {
        width: 92%;
        margin-right: 2%;
        margin-top: 2%;
        color: #f6f0e6;
        font-size: 6vw;
    }
    #sub-title2 {
        font-family: "aduma";
        margin-top: 12%;
        margin-right: 2%;
        color: #f6f0e6;
        font-weight: bolder;
        font-size: 10vw;
    }
    #main-title {
        color: #f6f0e6;
        margin-right: 2%;
        font-family: "aduma";
        font-size: 8vw;
        margin-top: 25%;
    }
    #sub-title {
        color: #f6f0e6;
        margin-right: 2%;
        font-size: 15vw;
        font-family: "aduma";
        font-weight: bold;
        margin-top: 0%;
    }

</style>