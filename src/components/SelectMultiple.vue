<template>
    <div id="select-multiple">
      <div id="bg" :style="{background: bgColor}">
        <div id="instruction">{{ title }}</div>
        <div v-for="(option, index) in options" :key="index" class="answer" :id="'opt' + (index)" @click="selectOpt">
          <img src="../assets/media/checkbox.png" alt="multiple-choice" class="check-box">
          <img
            v-if="selectedArr.includes(index)"
            src="../assets/media/check.svg"
            alt="checkmark"
            class="checkmark"
            :class="{ correct: correctFeedback[index] === true, incorrect: correctFeedback[index] === false }"
          />
          <div class="multiple-choice">{{ option }}</div>
        </div>
        <div id="checkBtn" @click="checkAns">{{ btnText }}</div>
      </div>
    </div>
  </template>
  
  <script>
  import json from "../../text.json";
  export default {
    name: "select-multiple",
    props: ["questionNum"],
    computed: {
      options() {
        return json.selectMultiple[this.questionNum].options;
      },
      title() {
        return json.selectMultiple[this.questionNum].title;
      },
      correctAns() {
        return json.selectMultiple[this.questionNum].correctAns;
      }
    },
    data() {
      return {
        selectedArr: [],
        btnText: "בדוק אותי",
        bgColor: "#fce9a9",
        correctFeedback: {}
      };
    },
    methods: {
      selectOpt(event) {
        let selectedOption = Number(event.currentTarget.id.charAt(3));
        if (!this.selectedArr.includes(selectedOption)) {
          if (this.selectedArr.length >= 3) {
            alert("סמן שלוש אפשרויות בלבד");
          } else {
            this.selectedArr.push(selectedOption);
          }
        } else {
          this.selectedArr = this.selectedArr.filter(item => item !== selectedOption);
        }
        this.correctFeedback = {}; // Reset feedback on selection change
      },
      checkAns() {
        const sortedArr1 = [...this.selectedArr].sort((a, b) => a - b);
        const sortedArr2 = [...this.correctAns].sort((a, b) => a - b);
  
        if (this.btnText === "בדוק אותי") {
          this.correctFeedback = {};
          for (const selectedIndex of this.selectedArr) {
            if (this.correctAns.includes(selectedIndex)) {
              this.correctFeedback[selectedIndex] = true;
            } else {
              this.correctFeedback[selectedIndex] = false;
            }
          }
  
          if (JSON.stringify(sortedArr1) !== JSON.stringify(sortedArr2)) {
            this.btnText = "תנסה שוב";
          } else {
            this.btnText = "מטורףף";
          }
        } else {
          this.btnText = "בדוק אותי";
          this.bgColor = "#fce9a9";
          this.selectedArr = [];
          this.correctFeedback = {};
        }
      }
    }
  };
  </script>
  
  <style scoped>
  #select-multiple {
    margin: 0;
    height: fit-content;
    margin-bottom: 10%;
    width: 100vw;
    position: relative;
    top: 0;
    right: 0;
  }
  #bg {
    list-style-type: none;
    padding: 1%;
    margin: auto;
    margin-top: 10%;
    margin-bottom: 0px;
    background-color: #fce9a9;
    border-radius: 1vh;
    width: 95vw;
  }
  #instruction {
    color: #001d3d;
    font-size: 8vw;
    margin: 2%;
    font-weight: 560;
    font-family: "aduma";
  }
  .answer {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    margin-bottom: 1.5vh;
    justify-content: start;
    align-items: center;
    position: relative; /* To position the checkmark */
  }
  .check-box {
    height: 5vh;
    margin-left: 3vw;
    margin-right: 3%;
  }
  .multiple-choice {
    background-color: #ffc300;
    margin: 1%;
    padding: 1vh;
    border-radius: 1vh;
    font-size: 2.5vh;
    text-align: start;
    color: #001d3d;
  }
  
  .checkmark {
    height: 4vh; /* Adjust size as needed */
    position: absolute;
    right: 3vw; /* Align with the checkbox */
  }
  
  .checkmark.correct {
    filter: invert(54%) sepia(97%) saturate(313%) hue-rotate(86deg) brightness(97%) contrast(94%); /* Green color */
  }
  
  .checkmark.incorrect {
    filter: invert(16%) sepia(99%) saturate(6681%) hue-rotate(357deg) brightness(98%) contrast(119%); /* Red color */
  }
  
  #checkBtn {
    margin-top: 6%;
    margin-right: 1%;
    background-color: #001d3d;
    font-family: "aduma";
    color: #ffc300;
    font-size: 8vw;
    border-radius: 1.5vh;
    font-weight: 580;
    width: 35vw;
    text-align: center;
    padding: 2%;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  }
  </style>