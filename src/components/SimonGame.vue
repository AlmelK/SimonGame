<template>
<div class="root">
<div class="game-content">
    <div class="btn-container">

        <button id="yellow"></button>
        <button id="green"></button>
        <button id="red"></button>
        <button id="blue"></button>

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
        <button>Start</button>
      </div>
    </div>

  </div>
</div>
  
</template>
<script>
export default {
  data() {
    return {
      difficulty: "",
    };
  },
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
            border: none
            cursor: pointer           

        #red
            background: #ff5050     
            
            &:hover
                box-shadow: 1px 1px 2px 3px red
                transition: .2s     

        #green
            background: #6f9

            &:hover
                box-shadow: 1px 1px 2px 3px green
                transition: .2s 

        #yellow
            background: #ffff44

            &:hover
                box-shadow: 1px 1px 2px 3px yellow
                transition: .2s 

        #blue
            background: #00ccff

            &:hover
                box-shadow: 1px 1px 2px 3px blue
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