<template>
  <div id="bingo-grid">
    <van-grid :column-num="5" :gutter="5" :square="true" class="grid-wrapper">
      <template v-for="cell_data in grid_data">
        <van-grid-item :key="cell_data">
          <Cell
            :cellNum="cell_data"
            :cellText="grid_text[cell_data]"
            @correct="addBlock"
            :reset-flag="reset"
          />
        </van-grid-item>
      </template>
    </van-grid>
  </div>
</template>

<script>
import { Grid, GridItem, Dialog, Circle } from "vant";
import Cell from "./Cell";


export default {
  name: "bingo-grid",
  components: {
    [Grid.name]: Grid,
    [GridItem.name]: GridItem,
    Cell: Cell,
    [Circle.name]: Circle
  },
  data() {
    return {
      currentSelected: [],
      grid_data: [],
      grid_text: [],
      reset: false,
      circleColor: "whilte",
      bingo:[[1,2,3,4,5],[6,7,8,9,10],[11,12,13,14,15],[16,17,18,19,20],[21,22,23,24,25]]
    };
  },
  methods: {
    gridNumbToText() {
      let hub = [
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        10,
        11,
        12,
        13,
        14,
        15,
        16,
        17,
        18,
        19,
        20,
        21,
        22,
        23,
        24,
        25
      ];
      //Crate list of text
      //Create list of 25 of the texts and match then to a number
      // eslint-disable-next-line
      this.grid_data = hub;
      let text = [
        "Can you hear me?",
        "Kids or animals making noise in the background",
        "Oops, I was on mute",
        "I hear myself in the echo",
        "Someone who thinks they are on mute and starts a conversation",
        "Static noise",
        "Can you go back a slide?",
        "Can everyone else be on mute?",
        "You are breaking up!",
        "I need to step away for a sec.",
        "Lets wait till everyone gets here.",
        "Can you repeat that?",
        "My internet connection is really bad",
        "Can you guys see my screen?",
        "Hello....Hello",
        "Sorry, No you go first.",
        "My video is not working",
        "Weird video camera angle",
        "Lets turn off video, maybe that will help",
        "$Free space$",
        "Bad Voice Quality",
        "Bad Video Quality",
        "Someone makes a Corona reference",
        "Someone Coughs",
        "Someone in pyjamas",
        "Someone else walks past camera",
        "Arriving early and waiting for the meeting to start"
      ];
      var currentIndex = text.length, temporaryValue, randomIndex;

      // While there remain elements to shuffle...
      while (0 !== currentIndex) {

        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        // And swap it with the current element.
        temporaryValue = text[currentIndex];
        text[currentIndex] = text[randomIndex];
        text[randomIndex] = temporaryValue;
      }
      this.grid_text = text.slice(0,26);
    },
    addBlock(blockNumber) {
      if(this.currentSelected.indexOf(blockNumber) === -1) {
        this.currentSelected.push(blockNumber)
        this.currentSelected.sort()
      }
      var i;
      var contains = false;
      //Row Bingo
      for (i=0; i<this.bingo.length; i++){
        if (this.bingo[i].every(elem => this.currentSelected.indexOf(elem) > -1)){
          contains = true
        }
      }
      //Colum Bingo
      for (i=0; i<this.bingo.length; i++){
        var col = [];
        var j;
        for (j=0; j<this.bingo.length; j++){
          col.push(this.bingo[j][i])
        }  
        if (col.every(elem => this.currentSelected.indexOf(elem) > -1)){
          contains = true
        }
      }
      //Cross Bingo
      var cor = [[1,7,13,19,25],[5,9,13,17,21]];
      for (i=0; i<cor.length; i++){
        if (cor[i].every(elem => this.currentSelected.indexOf(elem) > -1) && this.currentSelected.length >= 5){
          contains = true
        }
      }
      if (contains) {
        // finished success
        Dialog.alert({
          title: "Congratulations!!!",
          message: `Bingo!!!`
        }).then(() => {
          this.gridNumbToText();
          this.reset = !this.reset;
          this.circleColor = "white";
          this.currentSelected = [];
        });
      }
    }
  },
  mounted() {
    this.gridNumbToText();
    this.currentSelected = [];
    this.reset = !this.reset;
  }
};
</script>

<style>
.van-grid-item__content {
  padding: 0;
  max-height: 150px;
  max-width: 150px;
}
.cell {
  background-color: #ffe0b2;
  max-height: 100px;
  border: 1px solid black;
  vertical-align: center;
  align-content: center;
}
.num {
  display: inline-block;
  margin: auto auto;
}
.logo {
    padding-top: 23px;
    width: 100px;
    height: 100px;
}
.grid-wrapper {
    padding-top: 10px;
    max-width: 800px;
}
#bingo-grid {
    margin-left: 30%;
    margin-right: 30%;
}

</style>
