<template>
    <div id="positions-handler">
        <discovery :pageNum="pageNum" :contentNum="contentNum" v-if="contentNum === 1" @back-to-menu="backToMenu"></discovery>
        <fire :pageNum="pageNum" :contentNum="contentNum" v-if="contentNum === 2" @back-to-menu="backToMenu"></fire>
        <test :pageNum="pageNum" :contentNum="contentNum" v-if="contentNum === 3"></test>

    </div>

</template>

<script>
import json from "../../text.json";
import Discovery from "@/components/Discovery";
import Fire from "@/components/Fire";
import Test from "@/components/Test";

export default {
    name: "positions-handler",
    props:["contentNum", "pageNum"],
    components: {
        Discovery,
        Fire,
        Test
    },
    data() {
        return {
            
        }
    },
    methods: {
        backToMenu() {
            this.$emit('back-to-menu');
        }
    },
    computed: {

    }
}

</script>

<style scoped>
    @font-face {
        font-family: "aduma";
        src: url("../assets/fonts/Aduma Regular.ttf");
    }
    #positions-handler {
        margin: 0%;
        height: 100%;
        width: 100vw;
        position: absolute;
        top: 0;
        right: 0;
        
    }

</style>