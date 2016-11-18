---
layout: post
comments: true
title:  "A simple 21 game i JavaScript code"
date:   2016-11-16 20:41:32
---
A simple 21 card game I made as an examination in __1DV021__ course.

<!--break-->

{% highlight ruby %}
/**
 *
 * Card Game 21
 *
 * @author jimmybengtsson
 * @version 1.0.1
 *
 */

'use strict';

// Skapa kort

function Card(value, number, color) {
  this.value = value;
  this.number = number;
  this.color = color;
  this.card = color + number;

}

// Skapa en hel kortlek med värden.

function Deck() {

  this.value = [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14];
  this.number = ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A'];
  this.color = ['♠', '♣', '♥', '♦'];
  this.fullDeck = [];
  for (let i = 0; i < this.color.length; i++) {
    for (let j = 0; j < this.number.length; j++) {
      this.fullDeck.push(new Card(this.value[j], this.number[j], this.color[i]));
    }
  }
}

// Använder mig av Fisher-Yates metod för att  blanda korten.

Array.prototype.shuffle = function() {

  let theLength = this.length - 1;
  let toSwap;
  let temp;
  for (let i = theLength; i > 0; i--) {
    toSwap = Math.floor(Math.random() * i);
    temp = this[i];
    this[i] = this[toSwap];
    this[toSwap] = temp;
  }
  return this;
};

let newDeck = new Deck();
let finaleDeck = newDeck.fullDeck.shuffle();

// Dela kort. Ta det första kortet i arrayen (kortleken).

function Deal() {
  if (finaleDeck.length > 1) {
    return finaleDeck.shift();
  }
}

// Skapa en spelare.

function Player(cards = []) {

  // Skapa en hand. I settern har jag med att det ska dras ett kort så länge summan är under 16.

  Object.defineProperty(this, 'cards', {
    get: function() {
      return cards;
    },

    set: function(value) {
      value.push(new Deal(), new Deal());

      let score = function() {
        let i;
        let score = 0;
        let cardValue = 0;
        let aces = 0;

        for (i = 0; i < value.length; i++) {
          cardValue = value[i].value;
          if (cardValue === 14) {
            aces += 1;
          }
          score += cardValue;
        }

        while (score > 21 && aces > 0) {
          score -= 13;
          aces -= 1;
        }
        return score;
      };

      while (score() < 16 && value.length < 5) {
        value.push(new Deal());
      }

      cards = value;
    }
  });

  this.cards = cards;

  // Sammanlagda poängen för korten på handen.

  Object.defineProperty(this, 'score', {
    get: function() {
        let i;
        let score = 0;
        let cardValue = 0;
        let aces = 0;

        for (i = 0; i < cards.length; i++) {
          cardValue = cards[i].value;
          if (cardValue === 14) {
            aces += 1;
          }
          score += cardValue;
        }

        while (score > 21 && aces > 0) {
          score -= 13;
          aces -= 1;
        }
        return score;
      }
  });

  // Visar aktuell spelhand så som jag vill skriva ut den.

  Object.defineProperty(this, 'hand', {
    get: function() {
      let result = [];
      for (let i = 0; i < cards.length; i++) {
        if (cards[i].card) {
          result.push(cards[i].card);
        }
      }
      return result.join('  ');
    }
  });
}

// Skapa ett nytt spel.

function Game() {

  let _player = new Player();
  let _dealer = new Player();

  // Spelarens hand.

  Object.defineProperty(this, 'player', {
    get: function() {
      return _player.hand;
    }
  });

  // Givens hand.

  Object.defineProperty(this, 'dealer', {
    get: function() {
      return _dealer.hand;
    }
  });

  // Spelarens poäng.

  Object.defineProperty(this, 'playerScore', {
    get: function() {
      return _player.score;
    }
  });

  // Givens poäng.

  Object.defineProperty(this, 'dealerScore', {
    get: function() {
      return _dealer.score;
    }
  });

  // Spelaren har över 21.

  Object.defineProperty(this, 'playerBusted', {
    get: function() {
      return _player.score > 21;
    }
  });

  // Given har över 21.

  Object.defineProperty(this, 'dealerBusted', {
    get: function() {
      return _dealer.score > 21;
    }
  });
}

// Få ihop allt till en sträng som visas.

Game.prototype.toString = function() {

  if (this.playerBusted === true) {
    return '\n' + 'Player: ' + this.player + ' (' + this.playerScore + ') ' + 'Busted!' + '\n' + '\n' +
        'Dealer: ---' + '\n' + '\n' + 'Dealer wins!';
  }
  else if (this.playerScore === 21) {
    return '\n' + 'Player: ' + this.player + ' (' + this.playerScore + ') ' + '\n' + '\n' +
      'Dealer: ---' + '\n' + '\n' + 'Player wins!';
  }
  else if (this.playerBusted === false && this.dealerBusted === true) {
    return '\n' + 'Player: ' + this.player + ' (' + this.playerScore + ')' + '\n' + '\n' +
      'Dealer: ' + this.dealer + ' ' + ' (' + this.dealerScore + ') ' + 'Busted!' + '\n' + '\n' + 'Player wins!';
  }
  else if (this.playerScore > this.dealerScore || this.player.length === 5 && this.playerScore < 21) {
    return '\n' + 'Player: ' + this.player + ' (' + this.playerScore + ')' + '\n' + '\n' +
      'Dealer: ' + this.dealer + ' ' + ' (' + this.dealerScore + ') ' + '\n' + '\n' + 'Player wins!';
  }
  else {
    return '\n' + 'Player: ' + this.player + ' (' + this.playerScore + ')' + '\n' + '\n' +
      'Dealer: ' + this.dealer + ' ' + ' (' + this.dealerScore + ') ' + '\n' + '\n' + 'Dealer wins!';
  }
};

let letsPlay = new Game();
console.log(letsPlay.toString());
{% endhighlight %}

