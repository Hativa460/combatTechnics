<template>
    <div id="final">
        <div v-if="grade>=80" id="main-title" class="animate__animated animate__backInDown">כל הכבוד! סיימת!</div>
        <div v-if="grade<80" id="main-title-lowGrade" class="animate__animated animate__backInDown">סיימת! אך נראה שצריך לחזור על החומר..</div>
        <div id="main-title" class="animate__animated animate__backInDown"> ציונך הוא: {{ grade }}</div>
        <button @click="nextPage" id="start-btn" class="animate__animated animate__backInUp">מה אומר? שוב?</button>
    </div>
</template>

<script>
export default {
    name: "final-page",
    props:["grade"],
    data() {
        return {
           
        }
    },
    methods: {
        nextPage() {
            this.$emit('again');
        }
    }
}
</script>

<style scoped>
@font-face {
  font-family: "aduma";
  src: url("../assets/fonts/Aduma Regular.ttf");
}
#final {
    margin: 0%;
    height: 100%;
    width: 100vw;
    position: absolute;
    top: 0;
    right: 0;
}
#main-title {
    text-align: center;
    color: #f6f0e6;
    font-family: "aduma";
    font-weight: bold;
    font-size: 17vw;
    margin: 2%;
    margin-top: 40%;
}
#main-title-lowGrade {
    text-align: center;
    color: #f6f0e6;
    font-family: "aduma";
    font-weight: bold;
    font-size: 17vw;
    margin: 2%;
    margin-top: 30%;
}
#start-btn {
    background-color: #ffc300;
    color: #001d3d;
    display: block;
    font-family: "aduma";
    font-size: 10vw;
    border-radius: 3vw;
    margin: auto;
    margin-top: 7%;
    padding: 2.5%;
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5vw 15vw;
}

</style>