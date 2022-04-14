<template>
<div class="root">

<audio src="../assets/sounds/1.mp3" ref="sound1"></audio>
<audio src="../assets/sounds/2.mp3" ref="sound2"></audio>
<audio src="../assets/sounds/3.mp3" ref="sound3"></audio>
<audio src="../assets/sounds/4.mp3" ref="sound4"></audio>

<div class="game-content">
    <div class="btn-container">
        <button 
        id="yellow" 
        :class="{highlight: hlYellow}"
        @click="userInput(3)"></button>
        <button 
        id="green" 
        :class="{highlight: hlGreen}"
        @click="userInput(2)"></button>
        <button
        id="red" 
        :class="{highlight: hlRed}"
        @click="userInput(1)"></button>
        <button 
        id="blue" 
        :class="{highlight: hlBlue}"
        @click="userInput(4)"></button>
    </div>
    <div class="game-settings">
      <div class="choose-level">
        <div class="radio-form">
          <input type="radio" value="easy" id="easy_level" v-model="difficulty" />
          <label for="easy_level">Easy</label>
        </div>      
        <div class="radio-form">
          <input type="radio" value="normal" id="normal_level" v-model="difficulty"/>
          <label for="normal_level">Normal</label>        
        </div>
        <div class="radio-form">
          <input type="radio" value="hard" id="hard_level" v-model="difficulty" />
          <label for="hard_level">Hard</label>
        </div>
      </div>

      <div class="start-game">
        <button @click="start">Start</button>
      </div>
    </div>

  </div>
</div>
  
</template>
<script>
export default {
  data() {
    return {
      difficulty: "easy",
      started: false, //did the game start
      gamePlay: false, //check if the game make a move
      allowInput: false,//allow user input
      isWin: false,

      hlRed: false, //highlight for red button when it is in focus
      hlYellow: false, //highlight for yellow button when it is in focus
      hlGreen: false,//highlight for green button when it is in focus
      hlBlue: false, //highlight for blue button when it is in focus

      count: 0,
      roundKol: 20,
      
      series: [],
      userInputs: [],
    };
  },
  computed: {
    //Show current count
    showCount() {
      if (this.count == 0) 
        return "0"
      else
        return this.count
    }
  },
  methods:{
    //for random sound selection
    randomTone() {
      return Math.floor(Math.random() * 4) + 1
    },
    //start of the game
    start() {
      if (this.count == 0) {
        this.started = true //game is started
        this.addTone() //add tone to game series
        this.playSeries() //play game series
      }
    },
    addTone() {
      this.count++
      this.series.push(this.randomTone())
    },
    playSeries() {
      this.allowInput = false
      this.gamePlay = true
      let self = this
      let delay = 500
      this.series.forEach(function(tone, index, array) {
        if(index == array.length - 1)
          setTimeout(function() {
            if (self.started) {
              self.playTone(tone)
              self.allowInput = true
              self.gamePlay = false
            }
          }, delay)
          else
            setTimeout(function() {self.playTone(tone)}, delay)
          delay += 1000
      })      
      this.gamePlay = false
    },

    clearHighLights() {
      this.hlRed = false
      this.hlYellow = false
      this.hlGreen = false
      this.hlBlue = false
    },

    userInput(tone){
      if(!this.allowInput)
        return
      this.playTone(tone)
      this.userInputs.push(tone)

      //if user made a mistake
      if(this.userInputs[this.userInputs.length - 1] != this.series[this.userInputs.length - 1]){
        this.userInputs = []
        this.allowInput = false
        console.log("Wrong :(")
      }
      //if this is the last round
      if (this.userInputs.length == this.series.length) {
        let self = this
        this.userInputs = []
        if (this.series.length == this.roundKol){
          setTimeout(this.winnerSet, 500)
        } else {
          setTimeout(function() {
            self.addTone()
            self.playSeries()
          }, 1000)
        }
      }
    },
    playTone(tone){
      switch(tone) {
        case 1:
          this.$refs.sound1.pause()
          this.$refs.sound1.currentTime = 0
          this.$refs.sound1.play()
          this.hlRed = true
          break;
        case 2:
          this.$refs.sound2.pause()
          this.$refs.sound2.currentTime = 0
          this.$refs.sound2.play()
          this.hlGreen = true
          break;
        case 3:
          this.$refs.sound3.pause()
          this.$refs.sound3.currentTime = 0
          this.$refs.sound3.play()
          this.hlYellow = true
          break;
        case 4:
          this.$refs.sound4.pause()
          this.$refs.sound4.currentTime = 0
          this.$refs.sound4.play()
          this.hlBlue = true
          break;
      }
      if (!this.isWin)
        setTimeout(this.clearHighLights, 750)
    },
    winnerSet() {
      this.isWin = true
      console.log("You win!")
    }
  }
  
};
</script>
<style scoped lang="sass">
.root
  margin: 0 auto
  max-width: 85%
  background: #eee
  padding: 25px 30px
  border-radius: 15px
  display: flex
  justify-content: center

  .game-content
    display: flex

    .btn-container
        display: grid
        grid-gap: 10px
        grid-template-rows: 1fr 1fr
        grid-template-columns: 1fr 1fr 
        max-width: 100%
        justify-content: center
        margin-right: 40px
        margin-left: 40px

        button
            width: 100px
            height: 100px
            cursor: pointer           

        #red
          background: #ff5050     
            
        #red.highlight
            background: #8b0000
            transition: .2s

        #green
          background: #6f9

        #green.highlight
          background: green
          transition: .2s

        #yellow
          background: #ffff44

        #yellow.highlight
            background: orange
            transition: .2s

        #blue
          background: #00ccff

        #blue.highlight
          background: #0000cd
          transition: .2s
  .game-settings
      
      .choose-level
        display: block
        max-width: 100%
        padding: 20px

        .radio-form
          margin-bottom: 5px

          input, label
            vertical-align: middle
            margin-right: 5px

      .start-game
        max-width: 100%
        display: flex
        justify-content: center

        button
          width: 80%
          height: 30px
          background: #fff
          border: 2px solid #000
          border-radius: 15px
          cursor: pointer

          &:hover
            box-shadow: 1px 1px 1px 1px #000
            transition: .2s             
    


</style>