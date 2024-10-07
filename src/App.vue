<script setup>
import Block from "./Block.vue";
import { ref } from 'vue';

const board = ref(Array(9).fill(''));
const gameIsPayable = ref(true);
const currentPlayer = ref('X')



const handleClick = (index) => {
  // Vérifier si la case est déjà remplie
  if (board.value[index] !== '' || !gameIsPayable.value) return;
  board.value[index] = currentPlayer.value;

  if (winCondition()) {
    showResult(`Le joueur ${currentPlayer.value} a gagné !`);
  } else if (!board.value.includes('')) {
    showResult("Égalité");
    gameIsPayable.value = false;
  }
  else { currentPlayer.value = currentPlayer.value === "X" ? "O" : "X" }

  console.log(index);
}

const showResult = (message) => {
  alert(message);
  gameIsPayable.value = false
}

const winCondition = () => {
  const table = [
    [0, 1, 2],  // Ligne 1
    [3, 4, 5],  // Ligne 2
    [6, 7, 8],  // Ligne 3
    [0, 3, 6],  // Colonne 1
    [1, 4, 7],  // Colonne 2
    [2, 5, 8],  // Colonne 3
    [0, 4, 8],  // Diagonale 1
    [2, 4, 6],  // Diagonale 2
  ];

  return table.some((combination) => {
    const [a, b, c] = combination
    return board.value[a] &&
      board.value[a] === board.value[b] &&
      board.value[a] === board.value[c]
  })

}

const refrech = () => {
  location.reload();
}
</script>

<template>
  <button @click="refrech" class="btn">Reset</button>
  <div class="board">

    <Block v-for="(bloc, index) in board" :key="index" class="cell" :bloc="bloc" :data-index="index"
      @click="handleClick(index)" />
  </div>
  <article>
    <fieldset class="article">
      <legend>Règle jeu</legend>

      <p><strong>Tic-Tac-Toe (Morpion)</strong></p>
      <u>Matériel</u>
      <ul>
        <li>
          <p>Un plateau de 3x3 cases.</p>
        </li>
        <li>
          <p>Deux joueurs : l'un utilise "X" et l'autre "O".</p>

        </li>
      </ul>
      <p><u>Objectif</u></p>
      <ul>
        <li>
          Être le premier à aligner trois symboles (X ou O) horizontalement, verticalement ou en diagonale.
        </li>
      </ul>
      <p><u>
          Règles
        </u></p>
      <ol>
        <li>
          Tour de jeu : Les joueurs alternent leurs tours. Le premier joueur place son symbole dans une case vide.
        </li>
        <li>
          Conditions de victoire :
          <ul>
            <li>
              Un joueur gagne en ayant trois symboles alignés.
            </li>
            <li>
              Si toutes les cases sont remplies sans gagnant, c'est un match nul.
            </li>
          </ul>
        </li>
        <li>
          Fin du jeu : La partie se termine quand un joueur gagne ou qu'il y a match nul.
        </li>
      </ol>


    </fieldset>

  </article>
</template>

<style>
.btn {
  position: absolute;
  left: 4vh;
  top: 5vh;
  padding: 10px;
  border: 1px solid;
  border-radius: 10px;
  background-color: rgb(33, 18, 58);
  color: whitesmoke;
  cursor: pointer;
}

.btn:hover {
  background-color: whitesmoke;
  color: rgb(33, 18, 58);

}

body {
  background-color: rgb(33, 18, 58);
  color: whitesmoke;
  height: 100bh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.board {
  width: 610px;
  height: 574px;
  display: flex;
  flex-wrap: wrap;
  ;
  gap: 5px;
}

.cell {
  width: 190px;
  height: 190px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: sans-serif;
  font-size: 60px;
  border: 3px solid;
  border-radius: 10px;
  box-sizing: border-box;
  cursor: pointer;
}

.article{
  position: relative;
  left: 4vh;
  top: 5vh;
  padding: 10px;
  border: 1px solid;
  border-radius: 10px;
  background-color: rgb(33, 18, 58);
  color: whitesmoke;
  cursor: pointer;

}
</style>