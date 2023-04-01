// Curso de Engenharia de Software - UniEVANGÉLICA
// Disciplina de Programação Web
// Dev: ChatGPT
// Data: 01/04/2023

import React, { useState } from "react";
import "./styles.css";

const TicTacToe = () => {
const [board, setBoard] = useState(Array(9).fill(null));
const [player, setPlayer] = useState("X");
const [winner, setWinner] = useState(null);

// Define as possibilidades de vencer
const possibilities = [
[0, 1, 2],
[3, 4, 5],
[6, 7, 8],
[0, 3, 6],
[1, 4, 7],
[2, 5, 8],
[0, 4, 8],
[2, 4, 6]
];

// Função para checar o vencedor
const checkWinner = (board) => {
for (let i = 0; i < possibilities.length; i++) {
const [a, b, c] = possibilities[i];
if (board[a] && board[a] === board[b] && board[a] === board[c]) {
return board[a];
}
}
return null;
};

// Função para mudar o estado do tabuleiro
const handleClick = (index) => {
if (board[index] === null && winner === null) {
let newBoard = board;
newBoard[index] = player;
setBoard(newBoard);
setPlayer(player === "X" ? "O" : "X");
setWinner(checkWinner(newBoard));
}
};

// Função para resetar o jogo
const resetGame = () => {
setBoard(Array(9).fill(null));
setPlayer("X");
setWinner(null);
};

// Renderiza a célula do tabuleiro
const Cell = ({ index }) => {
return (
<div className="cell" onClick={() => handleClick(index)}>
{board[index]}
</div>
);
};

// Renderiza o tabuleiro
const Board = () => {
return (
<div className="board">
{board.map((cell, index) => (
<Cell key={index} index={index} />
))}
</div>
);
};

// Renderiza a mensagem de vitória ou empate
const Message = () => {
if (winner) {
return <div className="message">{Vencedor: ${winner}}</div>;
} else if (board.every((cell) => cell !== null)) {
return <div className="message">Empate!</div>;
} else {
return null;
}
};

// Renderiza o jogo da velha completo
return (
<div className="container">
<h1 className="title">Jogo da Velha</h1>
<Board />
<Message />
<button className="reset-button" onClick={() => resetGame()}>
Reiniciar Jogo
</button>
</div>
);
};

export default TicTacToe;
