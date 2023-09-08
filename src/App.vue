<script setup>
import { ref,} from 'vue'

const win_count_player1 = ref(0)
const draw_count_player1 = ref(0)
const loss_count_player1 = ref(0)

const win_count_player2 = ref(0)
const draw_count_player2 = ref(0)
const loss_count_player2 = ref(0)



const control_game = {
	'rock': {
		'rock': 'draw',
		'paper': 'lose',
		'scissors': 'win',
    'heart': 'lose'
	},
	'paper': {
		'rock': 'win',
		'paper': 'draw',
		'scissors': 'lose',
    'heart': 'lose'
	},
	'scissors': {
		'rock': 'lose',
		'paper': 'win',
		'scissors': 'draw',
    'heart': 'lose'
	},
  'heart': {
		'rock': 'win',
		'paper': 'win',
		'scissors': 'win',
    'heart': 'draw'
	}

}



const player1_choose = ref('');
const player2_choose = ref('');
const result = ref('');

const choiceImages = {
  'rock': 'OIP.jpg',
  'paper': 'OIP (1).jpg',
  'scissors': 'https://th.bing.com/th/id/OIP.IqxBu-6Y88u12814HE4b3AAAAA?pid=ImgDet&rs=1',
  'heart': 'https://png.pngtree.com/png-vector/20220428/ourmid/pngtree-smooth-glossy-heart-vector-file-ai-and-png-png-image_4557871.png',
};



function getRandomChoice() {
  const choices = ['rock', 'paper', 'scissors','heart'];
  return choices[Math.floor(Math.random() * choices.length)];
}

function display_answer() {
  player1_choose.value = getRandomChoice();
  player2_choose.value = getRandomChoice();

  const out_result = control_game[player1_choose.value][player2_choose.value];

  if (out_result === 'win') {
    win_count_player1.value++;
    loss_count_player2.value++;
    result.value = 'Player 1 win';
  } else if (out_result === 'lose') {
    win_count_player2.value++;
    loss_count_player1.value++;
    result.value = 'Player 2 win';
  } else {
    draw_count_player1.value++;
    draw_count_player2.value++;
    result.value = 'draw';
  }
}

function reset_round() {
  player1_choose.value = '';
  player2_choose.value = '';
  result.value = '';
  win_count_player1.value = 0;
  draw_count_player1.value = 0;
  loss_count_player1.value = 0;
  win_count_player2.value = 0;
  draw_count_player2.value = 0;
  loss_count_player2.value = 0;
}

</script>

<template>
  <div class="contrainer_all">
   

      <div class="contrainer_game">
        <div class="box_1" id="box_play1">
          Player 1 :  {{ player1_choose }}
          <img v-if="player1_choose" :src="choiceImages[player1_choose]" alt="Player 1 Choice" class="box_img"/>
        </div>
        <div class="box_2" id="box_play2">
          Player 2 :  {{ player2_choose }}
          <img v-if="player2_choose" :src="choiceImages[player2_choose]" alt="Player 2 Choice" class="box_img" />
        </div>
      </div>
<div>
    
      <div class="box_score"> win  {{ win_count_player1 }} : {{ win_count_player2 }}</div>   
</div>
    <div class="start_buttom">
      <button @click="display_answer" class="buttom_start"> Start the game. </button>
    </div>

  
    <div class="box_newgame">
      <button @click="reset_round" class="buttom_new"> reset </button>
    </div>

  </div>    

</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Itim&display=swap');


/*ALl body*/
:root {
  font-family: 'Itim', cursive;
  font-size: 24px;
  line-height: 1.5;
  font-weight: 400;
  color-scheme: light dark;

 
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: 100%;

}

#app {
  max-width: 1280px;
  margin:  auto;
  padding: 1rem;
  text-align: center;
}

*{
  padding: 10px;
}





.contrainer_game{
  display: grid;
  grid-template-columns: 1fr 1fr;
  margin-left: 300px;
  margin-right: 250px;
  padding: 20px;
  justify-content: center;
}










.buttom_new{
  padding: 20px;
  width: 7rem;
  height: 2.5rem;
  background-color: red;
  border-radius: 8px;
  border: 1px solid transparent;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.25s;
}

.buttom_start:hover{

 
  background-image: linear-gradient( 135deg, #F05F57 10%);
  
}


.buttom_start{
  padding: 20px;
  width: 9rem;
  height: 2.5rem;
  background-image: linear-gradient( 135deg, #81FBB8 10%, #28C76F 100%);
  border-radius: 8px;

  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.25s;
}



</style>