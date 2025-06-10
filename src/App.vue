<template>
  <div id="app">
    <div id="hamburger-menu" @click="showNav" v-if="openNav===false && page!==0 && clicked === false">
      <div class="bar"></div>
      <div class="bar"></div>
      <div class="bar"></div>
    </div>
    <img @click="backToPage" id="arrow" src="./assets/media/back-arrow.svg" alt="back" v-if="clicked === true && page!==0">
    <div id="background-gdud">196</div>
    <div id="logos">
      <img class="logo" src="./assets/media/logo460.svg" alt="460">
      <img class="logo" id="logo196" src="./assets/media/196.png" alt="196">
      <img class="logo" src="./assets/media/קקש.png" alt="קקש">
    </div>


    <open-page @next-page="increasePage" v-if="page===0 && openNav===false && clicked===false"></open-page>
    <nav-bar v-if="openNav===true && clicked===false" @close-menu="closeMenu" @switchPage="switchPage" :currPage="page-1"></nav-bar>
    <defenition @next-page="increasePage" v-if="page===1 && openNav===false && clicked===false"></defenition>
    <basic-premise @next-page="increasePage" v-if="page===2 && openNav===false && clicked===false"></basic-premise>
    <armor-fighting @next-page="increasePage" v-if="page===3 && openNav===false && clicked===false"></armor-fighting>
    <tank-department @next-page="increasePage" v-if="page===4 && openNav===false && clicked===false"></tank-department>
    <positions v-if="page===5 && openNav===false && clicked===false" @show-pos="showPositions" @next-page="increasePage"></positions>
    <moving v-if="page===6 && openNav===false && clicked===false" @next-page="increasePage"></moving>
    <operational v-if="page===7 && openNav===false && clicked===false" @next-page="increasePage"></operational>
    <positions-handler v-if="clicked===true" :contentNum="chosenContent" :pageNum="page" @back-to-menu="backToPage"></positions-handler>
    <graded-test v-if="page===8"  @next-page="scoreAndMovePage"  :contentNum="chosenContent"> </graded-test>
    <final-page v-if="page===9 && openNav===false && clicked===false" @again="again" :grade="gradeInTest"></final-page>
  </div>
</template>
 
<script>
import OpenPage from "@/components/OpenPage";
import FinalPage from "@/components/FinalPage";
import NavBar from "@/components/NavBar";
import Defenition from "@/components/Defenition";
import BasicPremise from "@/components/BasicPremise";
import ArmorFighting from "@/components/ArmorFighting";
import TankDepartment from "@/components/TankDepartment";
import Positions from "@/components/Positions";
import Moving from "@/components/Moving";
import Operational from "@/components/Operational";
import PositionsHandler from "@/components/PositionsHandler";
import GradedTest from "@/components/GradedTest";


export default {
  name: "app",
  components: {
    OpenPage,
    NavBar,
    Defenition,
    BasicPremise,
    ArmorFighting,
    TankDepartment,
    Positions,
    Moving,
    Operational,
    PositionsHandler,
    FinalPage,
    GradedTest
  },
  data(){
    return{
      page: 0,
      openNav: false,
      clicked: false,
      chosenContent: 0,
      gradeInTest: 0
    }
  },
  methods: {
    scoreAndMovePage(grade){
      this.gradeInTest = grade;
      this.page++;
    },
    increasePage() {
      this.page++;
    },
    again() {
      this.page = 0;
    },
    showNav() {
      this.openNav = true;
    },
    closeMenu() {
      this.openNav = false;
    },
    switchPage(index) {
      console.log(index);
      this.openNav = false;
      this.page = index;
    },
    showPositions(chosenNum) {
      this.chosenContent = Number(chosenNum);
      this.clicked = true;
    },
    backToPage() {
      this.clicked = false;
    }
  }
};
</script>

<style>

@font-face {
  font-family: "assistant";
  src: url("./assets/fonts/Assistant-Regular.otf");
}
@font-face {
  font-family: "aduma";
  src: url("./assets/fonts/Aduma Regular.ttf");
}



* {
  user-select: none; 
  font-family: "assistant";
  direction: rtl;
  overflow-x: hidden;
  -webkit-user-select: none;
}
  body{
    margin: 0%;
    width: 100vw;
    height: 100%;
    background-color: #001d3d;
    overflow-x: hidden;
  }
  #logos {
    position: fixed;
    top: 0%;
    left: 0%;
    z-index: 2;
    background-color: #001d3d;
    padding: 2%;
    width: 100%;
    display: flex;
    flex-wrap: nowrap;
    flex-direction: row-reverse;
    align-items: flex-end;
    justify-content: flex-start;
  }
  .logo {
    max-width: 100%;
    height: 8vh;
    margin-right: 4%;
  }
  #logo196 {
    margin-right: 0%;
  }

  #background-gdud {
    position: fixed;
    color: #f6f0e6;
    opacity: 0.1;
    font-family: "aduma";
    right: 50%;
    margin: 0%;
    bottom: 6%;
    font-weight: bold;
    font-size: 55vw;
    rotate: 270deg;
  }

  #hamburger-menu {
    position: fixed;
    top: 2%;
    right: 2%;
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    align-items: center;
    z-index: 3;
  }

  #arrow {
    position: fixed;
    top: 0%;
    right: 1%;
    z-index: 3;
    max-width: 100%;
    height: 10vh;
  }

  .bar {
    background: #ffc300;
    border-radius: 0.5vw;
    height: 1vh;
    width: 10vw;
    margin: 5%;
  }


</style>