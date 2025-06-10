<template>
    <div id="sortable">
      <div class="list">
        <div id="instruction">{{ title }}</div>
        <draggable class="list-group" :list="sortableData[questionNum].items" group="people">
          <div class="list-item" v-for="(element, index) in sortableData[questionNum].items" :key="index" :style="{background: getItemBgColor(index)}">
            {{ element }}
          </div>
        </draggable>
        <div id="checkBtn" @click="checkAns">{{ btnText }}</div>
      </div>
    </div>
  </template>
  
  <script>
  import draggable from 'vuedraggable';
  import json from "../../text.json";
  
  export default {
    name: "sortable-list",
    props: ["questionNum"],
    components: {
      draggable
    },
    data() {
      return {
        sortableData: json.sortable,
        correctAns: undefined,
        btnText: "בדוק אותי",
        bgColor: "#ffc300",
        itemColors: []
    };
    },
    computed: {
      title() {
        return json.sortable[this.questionNum].title;
      }
    },
    methods: {
        // checkAns() {
        //     // Access the list of items and correctList dynamically using the current questionNum
        //     const userList = this.sortableData[this.questionNum].items;
        //     const correctList = this.sortableData[this.questionNum].correctList;

        //     if (this.btnText !== "בדוק אותי") {
        //         // Reset the list to its original state
        //         this.$set(this.sortableData, this.questionNum, { 
        //         ...this.sortableData[this.questionNum],
        //         items: [...json.sortable[this.questionNum].items]  // reset the items array
        //         });
        //         this.correctAns = false;
        //         this.bgColor = "#ffc300";
        //         this.btnText = 'בדוק אותי';
        //     } else {
        //         if (JSON.stringify(userList) === JSON.stringify(correctList)) {
        //             this.correctAns = true;
        //             this.btnText = "אין עליך!";
        //             this.bgColor = "rgb(179, 241, 160)";
        //         } else {
        //             this.correctAns = false;
        //             this.bgColor= "rgb(247, 83, 83)";
        //             this.btnText="תנסה שוב...";
        //         }
        //     }
        // },
        checkAns() {
        const userList = this.sortableData[this.questionNum].items;
        const correctList = this.sortableData[this.questionNum].correctList;
  
        if (this.btnText !== "בדוק אותי") {
          // Reset the list to its original state
          this.$set(this.sortableData, this.questionNum, { 
            ...this.sortableData[this.questionNum],
            items: [...json.sortable[this.questionNum].items]  // reset the items array
          });
          this.correctAns = false;
          this.bgColor = "#ffc300";
          this.itemColors = [];
          this.btnText = 'בדוק אותי';
        } else {
          // Check each item in the list
          this.itemColors = userList.map((item, index) => {
            return item === correctList[index] ? "rgb(179, 241, 160)" : "rgb(247, 83, 83)";
          });
  
          if (JSON.stringify(userList) === JSON.stringify(correctList)) {
            this.correctAns = true;
            this.btnText = "אין עליך!";
          } else {
            this.correctAns = false;
            this.btnText = "תנסה שוב...";
          }
        }
      },
        getItemBgColor(index) {
        return this.itemColors[index] || this.bgColor;
        },
        onDragEnd() {
        // Reset the item colors to orange when the drag ends
        this.itemColors = Array(this.sortableData[this.questionNum].items.length).fill("#ffc300");
        this.btnText = "בדוק אותי";
      }

    }
    
  };
  </script>
  
  <style scoped>
  @font-face {
    font-family: "aduma";
    src: url("../assets/fonts/Aduma Regular.ttf");
  }
  
  #sortable {
    margin: 0;
    height: fit-content;
    margin-bottom: 10%;
    width: 100vw;
    position: relative;
    top: 0;
    right: 0;
  }
  
  .list {
    list-style-type: none;
    padding: 1%;
    margin: auto;
    margin-top: 10%;
    margin-bottom: 0px;
    background-color: #fce9a9;
    border-radius: 1vh;
    width: 95vw;
  }
  
  .list-item {
    color: #001d3d;
    padding: 3%;
    margin: auto;
    margin-top: 4%;
    margin-bottom: 4%;
    background-color: #ffc300;
    border-radius: 1vh;
    cursor: grab;
    width: 90%;
    font-size: 5.5vw;
    border: #001d3d dashed 0.5vh;
  }
  
  .list-item:active {
    cursor: grabbing;
  }
  
  #instruction {
    color: #001d3d;
    font-size: 8vw;
    margin: 2%;
    font-weight: 560;
    font-family: "aduma";
  }
  
  #checkBtn {
    margin: 2%;
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
  