<template>
    <div id="select-multiple-grade">
      <div id="bg" :style="{background: bgColor}">
        <div id="instruction">{{ title }}</div>
        <div v-for="(option, index) in options" :key="index" class="answer" :id="'opt' + (index)" @click="selectOpt">
          <img src="../assets/media/checkbox.png" alt="multiple-choice" class="check-box">
          <img src="../assets/media/check.svg" alt="checkmark" class="checkmark" v-if="selectedArr.includes(index)">
          <div class="multiple-choice">{{ option }}</div>
        </div>
        <!-- <div id="checkBtn" @click="checkAns">{{ btnText }}</div> -->
      </div>
    </div>
  </template>


<script>
import json from "../../text.json";
export default {
    name: "select-multiple-grade",
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
            selectedArr : [],
            btnText: "הגש",
            bgColor: "#fce9a9",
            isReadonly: false,
            points: 0,
        }
    },
    methods: {
        selectOpt(event) {
            let selectedOption = Number(event.currentTarget.id.charAt(3));
            if (!this.selectedArr.includes(selectedOption)) {
            if (this.selectedArr.length >= 3) {
                alert("סמן שלוש אפשרויות בלבד");
                return; // עצור את הפונקציה אם כבר נבחרו 3 אפשרויות
            } else {
                this.selectedArr.push(selectedOption);
             }
            } else {
                let newArr = [];
                for (let i = 0; i < this.selectedArr.length; i++) {
                    if (this.selectedArr[i] !== selectedOption) {
                    newArr.push(this.selectedArr[i]);
                    }
                }
                this.selectedArr = newArr;
            }
            this.calculatePoints(); // חשב את הנקודות לאחר כל שינוי
            this.$emit('points-updated', this.points); // שדר את הנקודות המעודכנות
            console.log(this.points+"בשאלה ראשונה");
        },
        calculatePoints() {
        this.points = 0;
        for (let i = 0; i < this.selectedArr.length; i++) {
          if (this.correctAns.includes(this.selectedArr[i])) {
            this.points += 4;     
          }
        }
       }
        // checkAns() {
        //     const sortedArr1 = this.selectedArr.sort();
        //     const sortedArr2 = this.correctAns.sort();
        //     for (let i = 0; i < this.correctAns.length; i++) {
        //         if (sortedArr1[i] === sortedArr1[i]) {
        //             this.points += 5;
        //         }
        //     }
        //         this.isReadonly = true;
        //         this.$emit('points-updated', this.points);
            
        // }

        }
    }
</script>

<style scoped>
#bg.readonly {
  pointer-events: none;
  opacity: 0.7;
  cursor: not-allowed;
}

#select-multiple-grade {
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
    height: 6vh;
    position: absolute;
    margin-right: 0%;
    margin-bottom: 2%;
    display: block;
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