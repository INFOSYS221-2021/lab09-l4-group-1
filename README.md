# Lab 9 Group 1

## Group members
* Jack McGrath
* Olivia Joe West
* Amos Lou

## Exercise 1
1. The GET method is a method used to retrieve data/information from the API you are requesting. 
If I wanted to create 2 decks then I would use the GET parameter "deck_count=2". The url would look like: https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=2

2. 
* Shuffle the cards
* Draw a card
* Reshuffle the cards
* Create brand new deck
* Create partial deck
* Create/add to piles
* Shuffle piles
* List cards in piles
* Draw cards from piles

3. https://deckofcardsapi.com/api/deck/new/?jokers_enabled=true

4. 
* Two cards are drawn from the deck. The cards are the King of Hearts and 8 of Clubs.

### Displaying deck id

``` 
let deck = {
    "success": true,
    "cards": [
        {
            "image": "https://deckofcardsapi.com/static/img/KH.png",
            "value": "KING",
            "suit": "HEARTS",
            "code": "KH"
        },
        {
            "image": "https://deckofcardsapi.com/static/img/8C.png",
            "value": "8",
            "suit": "CLUBS",
            "code": "8C"
        }
    ],
    "deck_id":"3p40paa87x90",
    "remaining": 50
}

deckID = deck.deck_id
console.log(deckID) 
```
### Displaying info for each card

```
let deck = {
    "success": true,
    "cards": [
        {
            "image": "https://deckofcardsapi.com/static/img/KH.png",
            "value": "KING",
            "suit": "HEARTS",
            "code": "KH"
        },
        {
            "image": "https://deckofcardsapi.com/static/img/8C.png",
            "value": "8",
            "suit": "CLUBS",
            "code": "8C"
        }
    ],
    "deck_id":"3p40paa87x90",
    "remaining": 50
}

deckID = deck.deck_id
for (var i = 0; i < deck.cards.length; i++) {
console.log("Card #" + (i + 1));
console.log("Value: " + deck.cards[i].value);
console.log("Suit: " + deck.cards[i].suit);
}
```

## Exercise 2
```
// Initialise the values at the start of the game
// Do not change this part!
let thisDeck;
let numOfHits = 0;
let sum = 0;

// Getting different elements from HTML
// Do not change this part!
const hitMeBtn = document.getElementById('hitMeBtn');
const restartBtn = document.getElementById('restartBtn');
const hitMeSum = document.getElementById('hitMeSum');
const hitMeCards = document.getElementById('hitMeCards');
hitMeBtn.addEventListener('click', playGame);
restartBtn.addEventListener('click', restartGame);

// Complete the following TODOs for each function

// This function shuffles a new deck of card
// and returns the deck id
async function createDeck() {
	
  // TODO 1: use the appropriate API to shuffle 
  // a new deck of card
  let response = await fetch('https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=1');

  if (response.status === 200) {
    let data = await response.json();

    // TODO 2: get the id of the deck from data
    deckID = data.deck_id;
    
    return deckID;
  }
}

// This function returns all available information
// about a card drawn from the deck created
async function getACard() {
  // TODO 3: use the appropriate API to draw one card 
  // from the deck created at the start of the game
  // Hint: use the variable thisDeck
  
  let response = await fetch('https://deckofcardsapi.com/api/deck/' + thisDeck + '/draw/?count=1');
  
  // retun card information
  // Do not change this
  if (response.status === 200) {
    let cardInfo = await response.json();
    return cardInfo;
  }
}

// This function returns the appropriate value
// based on cardInfo
function getValueFromCard(cardInfo) {
  // TODO 4: find the value and suit of the card
  let cardValue = cardInfo.cards[0].value;
  let cardSuit = cardInfo.cards[0].suit;
  
  // TODO 5: update the cardValue appropriately
  // if card is Jack, then set the cardValue to 11, etc
  if (cardValue == 'JACK') {
    cardValue = 11;
   }
   else if(cardValue == 'QUEEN'){
  	cardValue = 12;
  }
  else if (cardValue == 'KING'){
  	cardValue = 13;
   }
  else if (cardValue == 'ACE'){
    cardValue = 1;
  }
   
   
 
  // if a card is red, then the value will be negative
  // Do not change this.
  let posOrNeg = 1;
  if (cardSuit == 'DIAMONDS' || cardSuit == 'HEARTS') {
    posOrNeg = -1;
  }
  
  return cardValue * posOrNeg;
}

// This function gets the image from cardInfo
// and updates the HTML
function updateCardImg(cardInfo) {
    // TODO 6: find the image of the card
  let imgUrl = cardInfo.cards[0].image;
  
  // update HTML. Do not change this.
  hitMeCards.innerHTML += "<img src='" + imgUrl + "' width='100' />";
}

// This function controls the flow of the game
// Do not change this function!
async function playGame() {
  // get a new deck of card if we just start the game
  if (numOfHits === 0) {
    thisDeck = await createDeck();
  }
  
  // update the number of hits and button
  numOfHits = numOfHits + 1;
  restartBtn.disabled = false;
  
  // get card information and image, and
  // update the sum of cards
  cardInfo = await getACard();
  updateCardImg(cardInfo);
  sum += getValueFromCard(cardInfo);
  
  // check if we have reached the end of the game, and
  // update HTML appropriately
  if (numOfHits > 4) {
    hitMeSum.innerHTML = "End of Game! Total value of your cards is " + sum;
    hitMeBtn.disabled = true;
  } else {
    hitMeSum.innerHTML = "Current total value of your cards is " + sum;
  }
}

// This function resets the game
// Do not change this function!
function restartGame() {
  numOfHits = 0;
  sum = 0;
  hitMeBtn.disabled = false;
  restartBtn.disabled = true;
  hitMeSum.innerHTML = "Click Hit Me! to start playing!"
  hitMeCards.innerHTML = "";
}
```
