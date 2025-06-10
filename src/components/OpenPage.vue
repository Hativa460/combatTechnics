<template>
    <div id="open-page">
        <div id="main-title">טכניקות קרביות- לחימת המחלקה</div>
        <button @click="nextPage" id="start-btn">יאללה מתחילים</button>
    </div>
</template>



<script>
export default {
    name: 'open-page',
    props: [],
    data() {
        return {

        }
    },
    methods: {
        nextPage() {
            this.$emit('next-page');
        }
    }
}
</script>

<style scoped>
@font-face {
  font-family: "aduma";
  src: url("../assets/fonts/Aduma Regular.ttf");
}

#open-page {
    margin: 0%;
    height: 100%;
    width: 100vw;
    position: absolute;
    top: 0;
    right: 0;
    /* background-color: rgb(189, 151, 100); */
}
#main-title {
    text-align: center;
    color: #f6f0e6;
    font-family: "aduma";
    font-weight: bold;
    font-size: 17vw;
    margin: 2%;
    margin-top: 60%;
}
#start-btn {
    background-color: #ffc300;
    color: #001d3d;
    font-family: "aduma";
    font-size: 10vw;
    border-radius: 3vw;
    position: absolute;
    margin-top: 7%;
    left: 50%;
    transform: translateX(-50%);
    padding: 2.5%;
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5vw 15vw;
    animation: scaling 1.1s linear infinite alternate;
    -webkit-animation: scaling 1.1s linear infinite alternate;
}
@keyframes scaling {
    from {
        scale: 1;
    }
    to {
        scale: 1.05;
    }
}
@-webkit-keyframes scaling {
    from {
        scale: 1;
    }
    to {
        scale: 1.05;
    }
}
</style>