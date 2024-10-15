
## Query Selector

**Query Selector Limitations**
Selects only the first occurrences if multiple occurrences present.
**Solution** - Query Selector All

```js
// by class name -> .
// by id name -> #

console.log(document.querySelector('.heading')); // <h1 class="heading">Guess a Number Game!</h1>
console.log(document.querySelector('.heading').textContent); // Guess a Number Game!
```

==**NOTE:**==
DOM and DOM methods are not a part of JavaScript. It is a part of Web API.

## Event Listener

```html
<input type="number" class="btn-input">
<input type="submit" class="btn-submit">
```

```js
// event listener
document.querySelector('.btn-submit').addEventListener('click', function () {
  console.log(document.querySelector('.btn-input').value);
});
```

## Manipulating CSS

```js
document.querySelector('body').style.backgroundColor = 'green';
```

## Setting Attributes

```js
document.querySelector('.btn-submit').setAttribute('disabled', true);
```

## GAME: Guess a number

Input from user a number and check with system generated random number. If guess of the user is wrong there is a penalty of 1 points. User top score is also saved.

```html
<!DOCTYPE html>
<body>
    <input type="submit" class='btn-restart' value="Restart">
    <h1 class="heading">Guess a Number Game!</h1>

    <p>Input a number between 1 to 20</p>
    <input type="number" class="txt-guess">
    <input type="submit" class="btn-submit" value="Guess">
    <h3 class="message" style="color: red;"></h3>
    <h3>Score: <span class="score"></span></h3>
    <h3>High Score: <span class="hscore"></span></h3>
</body>
<script src="script.js"></script>
</html>
```

```js
'use strict';

const number = Math.ceil(Math.random() * 20);
let score = 20;
let highScore = !localStorage.getItem('highScore')
  ? 0
  : localStorage.getItem('highScore');

let scoreSelector = document.querySelector('.score');
let hscoreSelector = document.querySelector('.hscore');
let messageSelector = document.querySelector('.message');
let restartBtnSelector = document.querySelector('.btn-restart');

scoreSelector.textContent = score;
hscoreSelector.textContent = highScore;

console.log(number);

const guess = () => {
  const guess = Number(document.querySelector('.txt-guess').value);

  if (!guess) {
    messageSelector.textContent = 'Please enter a number!';
    return;
  }

  if (guess > number) {
    score--;
    scoreSelector.textContent = score;
    messageSelector.textContent = 'Guess is High!';
  }

  if (guess < number) {
    score--;
    scoreSelector.textContent = score;
    messageSelector.textContent = 'Guess is Low!';
  }

  if (guess === number) {
    document.querySelector('body').style.backgroundColor = 'green';
    if (highScore < score) {
      highScore = score;
      localStorage.setItem('highScore', highScore);
    }
    hscoreSelector.textContent = highScore;
    messageSelector.textContent = 'You got it right. Yehhh!!!';
    document.querySelector('.btn-submit').setAttribute('disabled', true);
  }
};

document.querySelector('.btn-submit').addEventListener('click', guess);
document.querySelector('.btn-restart').addEventListener('click', function () {
  location.replace(location.href);
});

```


## Manipulating Classes

```html
<!DOCTYPE html>
<style>
    body{
        color: blue;
    }
    .hidden{
        display: none;
    }
</style>

<body>
    <div>
        <input type="button" class ="btn-show-modal" value="Modal Window 1">
        <p class="modal hidden">
            Modal 1
            <input type='button' class="btn-close" value="close">
        </p>
    </div>
    <div>
        <input type="button" class ="btn-show-modal" value="Modal Window 2">
        <p class="modal hidden">
            Modal 2
            <input type='button' class="btn-close" value="close">
        </p>
    </div>
    <div>
        <input type="button" class ="btn-show-modal" value="Modal Window 3">
        <p class="modal hidden">
            Modal 3
            <input type='button' class="btn-close" value="close">
        </p>
    </div>
</body>
<script src="script.js"></script>
</html>
```

```js
'use strict';

const showModalSeclector = document.querySelectorAll('.btn-show-modal');
const modelSelector = document.querySelectorAll('.modal');
const btnCloseSelector = document.querySelectorAll('.btn-close');

for (let i = 0; i < showModalSeclector.length; i++) {
  showModalSeclector[i].addEventListener('click', function () {
    modelSelector[i].classList.remove('hidden');
  });
}

for (let i = 0; i < btnCloseSelector.length; i++) {
  btnCloseSelector[i].addEventListener('click', function () {
    modelSelector[i].classList.add('hidden');
  });
}
```

## ESC Key Press Event

```js
document.addEventListener('keydown', function (e) {
  if (e.key === 'Escape') {
    // close the modal window
    for (let i = 0; i < modelSelector.length; i++) {
      modelSelector[i].classList.add('hidden');
    }
  }
});
```

## GAME: Pig Game

```html
<!DOCTYPE html>
<style>
    .color-change{
        background-color: green;
        color: antiquewhite;
    }
</style>

<body>
    <h1>Pig Game</h1>
    <hr/>
    <div class="area_player_1">
        <h2>Player 1</h2>
        <h2>Score: <span id="p1-score">6</span></h2>
        <h2>Current Score: <span id="p1-score-current">2</span></h2>
    </div>
    <hr/>
    <div class="dice_area">
        <h1 id="dice_outcome">5</h1>
        <input type="button" id="hold" value="Hold">
        <input type="button" id="roll" value="Roll">
    </div>
    <hr/>
    <div class="area_player_2">
        <h2>Player 2</h2>
        <h2>Score: <span id="p2-score">6</span></h2>
        <h2>Current Score: <span id="p2-score-current">2</span></h2>
    </div>
</body>
<script src="script.js"></script>
</html>
```

```js
const btn_roll = document.querySelector('#roll');
const btn_hold = document.querySelector('#hold');
const lbl_dice_outcome = document.querySelector('#dice_outcome');
const player1_area = document.querySelector('.area_player_1');
const player2_area = document.querySelector('.area_player_2');
const p1_curr_score = document.querySelector('#p1-score-current');
const p2_curr_score = document.querySelector('#p2-score-current');
const p1_score = document.querySelector('#p1-score');
const p2_score = document.querySelector('#p2-score');

// scores
let currentScoreP1 = 0;
let currentScoreP2 = 0;
let scoreP1 = 0;
let scoreP2 = 0;
p1_curr_score.textContent = 0;
p2_curr_score.textContent = 0;
p1_score.textContent = 0;
p2_score.textContent = 0;

// player 1 starts
let turn = true;
player1_area.classList.add('color-change');

// get random number from 1 to 6
const roll_a_dice = () => {
  return Math.trunc(Math.random() * 6 + 1);
};

btn_roll.addEventListener('click', function () {
  const dice = roll_a_dice();
  lbl_dice_outcome.textContent = dice;
  if (turn) {
    // add to the current score
    currentScoreP1 = currentScoreP1 + dice;
    p1_curr_score.textContent = currentScoreP1;

    if (dice === 1) {
      alert('Player 2 wins...');
      location.replace(location.href);
    }
  }
  if (!turn) {
    // add to the current score
    currentScoreP2 = currentScoreP2 + dice;
    p2_curr_score.textContent = currentScoreP2;

    if (dice === 1) {
      alert('Player 1 wins...');
      location.replace(location.href);
    }
  }
});

btn_hold.addEventListener('click', function () {
  // score
  if (turn == true) {
    scoreP1 = scoreP1 + currentScoreP1;
    p1_score.textContent = scoreP1;
    currentScoreP1 = 0;
    p1_curr_score.textContent = 0;
  }
  if (turn != true) {
    scoreP2 = scoreP2 + currentScoreP2;
    p2_score.textContent = scoreP2;
    currentScoreP2 = 0;
    p2_curr_score.textContent = 0;
  }
  // switch player
  turn = !turn;
  if (turn) {
    player1_area.classList.add('color-change');
    player2_area.classList.remove('color-change');
  }
  if (!turn) {
    player1_area.classList.remove('color-change');
    player2_area.classList.add('color-change');
  }
});

```


